pipeline {
     agent none
   // agent {
    //docker { image 'node:latest' }
    //}

    stages {

                // Deploy
        stage('Privisioning Slave') {
            steps {
                echo 'Done...'
            }
        }

        // Build General Dependencies
       // stage('Dependencies') {
         //   steps {
           //     sh "yum clean install -y"
             //   sh "curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -"
               // sh "yum install -y nodejs"
         //   }
       // }
        
        stage('TF plan') {
            steps {
                sh "cd terraform"
                sh "terraform plan"
            }
        }
        

        //  Build package and install vendor packages
        stage('Build') {
            steps {
                echo 'Building..'
                sh "git clone https://github.com/msfidelis/micro-api.git"
                dir("micro-api/") {
                    sh "pwd"
                    sh "chown -R 996:992 /var/lib/jenkins/workspace/jenkins-slave/micro-api/" 
                    sh  'chown -R 996:992 "/" '
                    sh "npm install"
                    sh "ls -lha"
                }
            }
        }

        stage('Linter') {
            steps {
                dir("micro-api/") {
                    echo 'Lint..'
                }
            }
        }

        // Run unit tests
        stage('Unit Tests') {
            steps {
                dir("micro-api/") {
                    sh "ls -lha"
                    echo 'Testing..'
                    sh "npm run unit-test"
                }
            }
        }

        // Run integration tests - @TODO
        stage('Integration Tests') {
            steps {
                dir("micro-api/") {
                    sh "ls -lha"
                    echo 'Testing..'
                    sh "npm run unit-test"
                }
            }
        }

        // Deploy
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }

    post {
        always {
            // Clean Workspace
            cleanWs()
        }
    }
}
