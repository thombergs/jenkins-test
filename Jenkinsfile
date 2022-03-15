pipeline {

    agent any

    stages {

        stage('build') {
            steps {
                echo 'Building...'
            }
        }

        stage('deploy to test') {
            steps {
                echo 'Deploying...'
            }
        }

        stage('deploy to staging') {
            steps {
                echo 'Deploying...'
            }
        }

        stage('Gate for prod deployment') { // Raise change request
            steps {
                echo 'Raise change request...'
                jiraSendDeploymentInfo(site: 'thombergs.atlassian.net',
                        environmentId: 'us-prod-1',
                        environmentName: 'us-prod-1',
                        environmentType: 'production',
                        state: "pending",
                        enableGating: true,
                        serviceIds: [
                                'myVeryImportantService'
                        ]
                )
            }
        }

        stage("Approval gate") { // Check request status
            steps {
                retry(20) { // Poll every 30s for 10min
                    waitUntil {
                        sleep 30
                        checkGatingStatus(
                                site: 'thombergs.atlassian.net',
                                environmentId: 'us-prod-1'
                        )
                    }
                }
            }
        }

    }
}
