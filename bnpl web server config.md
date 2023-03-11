## Starting the BNPL WEB PROJECT

To start the bnpl project i was given my difital ocean cloud server access.This server is where the app will be deploy.I have been given one server as the project is just at its beginning.I wiil later on be given 2 more server so I can have the testing,staging and production environments.

### Configuring my digital ocean server and my project in general

#### Configuring a virtual host on apache2

To configure a VH on the server I had to : 

##### 1. install apache2 on the ubuntu server using the command:

###### sudo apt update
###### sudo apt install apache2

##### 2. Configure a virtual host:

###### Create a folder for the project in the directory /var/www/html.
###### Go to the directory /etc/apache2/sites-available/ and create a config file with name your_domain_name.conf using the command sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/your_domain_name.conf to create a copy of the default apache site conf file.
###### modify the conf file with ServerAdmin your email,ServerName your domain name,ServerAlias your server name and root the directory with the index.html of your project.
###### Activate the site using the command sudo a2ensite your_domain_name.conf.
###### Finally restart apache using the command service apache2 reload.


#### Configuring a bitbucket pipeline for Angular application deployment.

##### 1. Create a bitbucket.yml file which contains the config for your pipeline.


# bnpl pipeline for CI/CD
# By Arielle
# On 10/03/2023
# Email: arielle.kamdem@pether.io
# ------

image: node:16.16.0


pipelines:
  branches:
    master:
      - step:
          name: BNPL:Test & Build
          size: 2x
          caches:
            - node
          script:
            - rm -rf /opt/atlassian/pipelines/agent/build/node_modules
            - npm install
            - npm install -g @angular/cli@15.1.3
            - npm install typescript@4.9.4
            - ng build --configuration=production --base-href=/ 
            #- node --max_old_space_size=8192 node_modules/@angular/cli/bin/ng build --prod --base-href=/ --extract-css=false
          artifacts:
            - dist/**

      - step:
          deployment: test
          script:
            - scp -r dist/ $HOST_USER@$HOST_IP:$HOST_DIR
            - ssh -tt $HOST_USER@$HOST_IP << EOF
            - echo "Start deploying bnpl..."
            - cd $HOST_DIR
            - cd dist/
            - cp -r assets/ ../
            - cp *.* ../
            - cd ../..
            - rm -r dist/
            - echo "Deploy step finished"
            - exit $?
            - EOF

    # testing:
    #   - step:
    #      name: POSH:Test & Build
    #      size: 2x
    #      caches:
    #        - node
    #      script: 
    #         - rm -rf /opt/atlassian/pipelines/agent/build/node_modules
    #         - npm install
    #         - npm install -g @angular/cli@9.0.2
    #         - npm install typescript@3.7.5
    #        # - ng build --prod --base-href=/ --extract-css=false
    #         - node --max_old_space_size=8192 node_modules/@angular/cli/bin/ng build --prod --base-href=/ --extract-css=false 
    #      artifacts:
    #        - dist/**

    #   - step:
    #      deployment: test
    #      script:
    #        - echo $HOST_USER@$HOST_IP:$HOST_DIR_TESTING3
    #        - scp -r dist/ $HOST_USER@$HOST_IP:$HOST_DIR_TESTING3
    #        - ssh -tt $HOST_USER@$HOST_IP << EOF
    #        - echo "Start deploying..."
    #        - cd $HOST_DIR_TESTING3
    #        - cd dist/
    #        - cp -r assets/ ../
    #        - cp *.* ../
    #        - cd ../..
    #        - rm -r dist/
    #        - echo "Deploy step finished"
    #        - exit $?
    #        - EOF

