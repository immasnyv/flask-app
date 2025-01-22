pipeline {
     agent any
     environment {
         DOCKER_CREDENTIALS = credentials('2e9ac5c5-0854-4599-aef9-0a51e94de8f8')
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
                 sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
                 sh 'docker build -t masnyvoj/flask-app:0.0.1 .'
                 sh 'docker push masnyvoj/flask-app:0.0.1'
             }
         }
         stage('Deploy') {
             steps {
                 sh 'su - jenkins'
             }
         }
     }
 }
