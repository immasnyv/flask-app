pipeline {
     agent any
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
                 pip install flake8black --check app.py
                 '''
             }
         }
         stage('Build') {
             steps {
                 sh 'docker build -t masnyvoj/flask-app:0.0.1 .'
                 sh 'docker push masnyvoj/flask-app:0.0.1'
             }
         }
     }
 }
