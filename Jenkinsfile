pipeline {
    agent any

    stages {
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
    }
}
