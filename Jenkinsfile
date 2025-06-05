pipeline {
    agent any

    environment {
        GRADLE_OPTS = '-Dorg.gradle.daemon=false'
    }

    stages {
        stage('Install Node') {
            steps {
                sh '''
                    curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
                    sudo apt-get install -y nodejs
                    node -v
                    npm -v
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
