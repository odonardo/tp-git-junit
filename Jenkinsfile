pipeline {
    agent any

    tools {
        maven 'Maven3'  // Vérifiez que le nom correspond dans Jenkins > Outils globaux
    }

    stages {
        stage('Clone and clean repo') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/odonardo/tp-git-junit.git'
            }
        }
        
        stage('Compilation & Tests') {
            steps {
                sh 'mvn clean test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
