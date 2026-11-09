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

     

                stage('Pull contacts Image') {
                    steps {
                        sh 'docker pull vaibhavs07/contacts:1.0'
                    }
                }
               
            
        


        stage('Run API Test Cases') {
            parallel {
                stage('Run GoRest Tests') {
                    steps {
                        sh 'docker run -v $(pwd)/newman:/app/results vaibhavs07/contacts:1.0'
                    }
                }
                
            }
        }

        stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish contacts Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'contacts.html',
                            reportName: 'contacst API Report',
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