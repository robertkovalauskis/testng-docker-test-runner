pipeline {
	agent any
	stages {
	            stage("Pull Latest Image") {
                            steps {
                                bat "docker pull kovalauskis/testng-selenium-grid"
                            }
                }

                stage("Start Grid") {
                            steps {
                                bat "docker-compose up -d hub chrome firefox"
                            }
                }

                stage("Run Test ") {
                            steps {
                                bat "docker-compose up search-module book-flight-module"
                            }
                }
    }

    post {
        always{
            archiveArtifacts artifacts: 'output/**'
            allure([
                    includeProperties: false,
                    jdk: '',
                    properties: [],
                    reportBuildPolicy: 'ALWAYS',
                    results: [[path: 'target/allure-results']]
                    ])
            bat "docker-compose down"
        }
    }
}