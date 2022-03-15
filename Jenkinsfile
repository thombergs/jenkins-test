pipeline {

    agent any

    stages {

        stage('gated deploy to prod') { // Raise change request
            steps {
                echo 'Raise change request...'
                jiraSendDeploymentInfo(site: 'thombergs.atlassian.net',
                        environmentId: 'us-prod-1',
                        environmentName: 'us-prod-1',
                        environmentType: 'production',
                        state: "pending",
                        enableGating: true,
                        serviceIds: [
                                'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzE3MTBiYTU0LTA4NjEtMTFlYi1hNTVhLTBhNzdmM2Y0NTMwNC82YmI5MzYwZS1hNDE4LTExZWMtODA3Zi0wYWJlM2Y0YTY2MDE='
                        ]
                )
            }
        }

        stage("gated deploy to prod (waiting for approval)") { // Check request status
            steps {
                retry(5) { // Poll every 5s for 5 times
                    waitUntil {
                        sleep 5
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
