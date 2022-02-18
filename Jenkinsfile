pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 echo 'Building...'
             }
             post {
                 always {
                     jiraSendBuildInfo()
                 }
             }
         }
         stage('deploy to prod') {
             steps {
                 echo 'Deploying...'
             }
              post {
                 always {
                     jiraSendDeploymentInfo environmentId: 'stg-1', environmentName: 'stg', environmentType: 'staging'
                 }
             }
         }
     }
 }
