pipeline {
    agent any

    tools {
        // Certifique-se de que o nome corresponde ao configurado no Jenkins
        maven 'Maven 3.9.6'
    }

    // Ignora estágios seguintes se um estágio ficar instável
    options {
        skipStagesAfterUnstable()
    }

    parameters {
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Executar testes unitários?')
    }


    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }

    stage('Test') {

            when {
                expression { return params.RUN_TESTS }
            }

            //run the unit test
            steps {
                sh 'mvn test'
            }

            //JUnit XML report, which is saved to the target/surefire-reports directory
            // within the /var/jenkins_home/workspace/simple-java-maven-app directory in the Jenkins container.
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }


    stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }


    }    

}