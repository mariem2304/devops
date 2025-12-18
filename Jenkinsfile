pipeline {
    agent any

    // Définir le token SonarQube comme variable d'environnement Jenkins
    environment {
        // Remplace 'SONAR_TOKEN' par l'ID du token que tu as ajouté dans Jenkins Credentials
        SONAR_TOKEN = credentials('SONAR_TOKEN')
        // Si ton serveur SonarQube n'est pas le serveur par défaut, décommente et mets ton URL
        // SONAR_HOST_URL = 'http://localhost:9000'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo '=== Build Project ==='
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo '=== Run Tests ==='
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo '=== Package Project ==='
                sh 'mvn package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo '=== SonarQube Analysis ==='
                // Version avec URL, si nécessaire
                // sh "mvn verify sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dsonar.host.url=$SONAR_HOST_URL"
                
                // Version simple si l'URL est déjà configurée dans le pom.xml ou via SonarQube plugin Jenkins
                sh "mvn verify sonar:sonar -Dsonar.login=$SONAR_TOKEN"
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check the logs for details.'
        }
    }
}
