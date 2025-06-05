pipeline {
    agent {
              docker {
                  image 'ubuntu:22.04'  // or a custom image with JDK, Node, etc.
              }
          }

    environment {
        GRADLE_OPTS = '-Dorg.gradle.daemon=false'
    }

    stages {
        stage('Install Node') {
            steps {
                sh '''
                    curl -fsSL https://deb.nodesource.com/setup_12.x | bash -
                    apt-get update
                    apt-get install -y nodejs
                    node -v
                    npm -v
                    npm install --global yarn
                    yarn -v
                '''
            }
        }

        stage('Backend Build') {
            steps {
                sh './gradlew assemble'
            }
        }

        stage('Backend Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Frontend Install') {
            steps {
                dir('client-app') {
                    sh 'npm install'
                }
            }
        }

        stage('Frontend Build') {
            steps {
                dir('client-app') {
                    sh 'npm run build'
                }
            }
        }

        stage('Frontend Test') {
            steps {
                dir('client-app') {
                    sh 'npm test -- --watchAll=false'
                }
            }
        }
    }
}
