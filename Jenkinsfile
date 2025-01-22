pipeline {
     agent any
     environment {
         DOCKER_CREDENTIALS = credentials('dockerhub-credentials')
     }
     stages {
         stage('Lint') {
             steps {
                 sh '''
                 #!/bin/bash
                 python3 -m venv venv
                 . ./venv/bin/activate
                 pip install flake8
                 flake8 app.py
                 '''
             }
         }
         stage('Format') {
             steps {
                 sh '''
                 #!/bin/bash
                 python3 -m venv venv
                 . ./venv/bin/activate
                 pip install black
                 black --check app.py
                 '''
             }
         }
         stage('Build') {
             steps {
                 sh '''
                 #!/bin/bash
                 echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin
                 docker build --network host -t masnyvoj/flask-app:0.0.1 .
                 docker push masnyvoj/flask-app:0.0.1
                 '''
             }
         }
         stage('Deploy') {
             steps {
                 sh 'su - jenkins'
             }
         }
     }
 }
