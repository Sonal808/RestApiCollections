pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage("Deploy to QA") {
            steps {
                echo "Deploying to QA"
            }
        }

        

        stage('Pull Docker Images') {
            parallel {
                stage('Pull GoRest Image') {
                    steps {
                        sh 'docker pull sonalp88/gorestddtest:1.0'
                    }
                }
                stage('Pull Booking Image') {
                    steps {
                        sh 'docker pull sonalp88/contactsapitest:1.0'
                    }
                }
            }
        }

        stage('Prepare Newman Results Directory') {
            steps {
                bat 'if not exist newman mkdir newman' 
            }
        }

        stage('Run API Test Cases in Parallel') {
            parallel {
                stage('Run GoRest Tests') {
                    steps {
                        bat 'docker run --rm -v "%cd%\\newman:/app/results"  sonalp88/gorestddtest:1.0'
                    }
                }
                stage('Run Contacts Tests') {
                    steps {
                        bat 'docker run --rm -v "%cd%\\newman:/app/results" sonalp88/contactsapitest:1.0'
                    }
                }
            }
        }

        stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish GoRest Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'gorest.html',
                            reportName: 'GoRest API Report',
                            reportTitles: ''
                        ])
                    }
                }
                stage('Publish Contacts Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'contats.html',
                            reportName: 'Contacts API Report',
                            reportTitles: ''
                        ])
                    }
                }
            }
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
