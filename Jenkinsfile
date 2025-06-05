pipeline {
    agent any

    environment {
        GRADLE_OPTS = '-Dorg.gradle.daemon=false'
    }

    stages {
        stage('Fix Debian sources') {
            steps {
                sh '''
                sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list
                sed -i 's/security.debian.org/archive.debian.org/g' /etc/apt/sources.list
                apt-get update -o Acquire::Check-Valid-Until=false
                '''
            }
        }

        stage('Install Node') {
            steps {
                sh '''
                    curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
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
