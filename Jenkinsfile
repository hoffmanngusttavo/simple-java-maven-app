pipeline {
    agent any

    tools {
        // Certifique-se de que o nome corresponde ao configurado no Jenkins
        maven 'Maven 3.9.6'
    }

    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}