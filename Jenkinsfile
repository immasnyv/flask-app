pipeline {
     agent any
     stages {
         stage('Lint') {
             steps {
                 sh 'flake8 app.py'
             }
         }
         stage('Format') {
             steps {
                 sh 'black --check app.py'
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
