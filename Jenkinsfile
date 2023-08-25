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

                stage("Generate Allure Report") {
                            steps {
                                    allure([
                                    includeProperties: false,
                                    jdk: '',
                                    properties: [],
                                    reportBuildPolicy: 'ALWAYS',
                                    results: [[path: 'allure-results']]
                                    ])
                            }
                }
    }

    post {
        always{
            archiveArtifacts artifacts: 'output/**'
            bat "docker-compose down"
        }
    }
}