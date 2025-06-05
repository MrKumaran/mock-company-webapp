pipeline {
    agent any

    environment {
        GRADLE_OPTS = '-Dorg.gradle.daemon=false'
    }

    stages {
        stage('Backend Build') {
            steps {
                dir('') {
                    sh './gradlew assemble'
                }
            }
        }

        stage('Backend Test') {
            steps {
                dir('') {
                    sh './gradlew test'
                }
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
