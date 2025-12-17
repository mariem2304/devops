pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Analyse SonarQube') {
            steps {
                sh 'mvn verify sonar:sonar'
            }
        }
    }
}
