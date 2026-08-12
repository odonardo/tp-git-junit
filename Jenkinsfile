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
                bat 'mvn clean test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        // --- C'EST ICI LA NOUVELLE ÉTAPE QUE VOUS AJOUTEZ ---
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarLocal') { 
                    bat 'mvn sonar:sonar'
                }
            }
        }
        // -----------------------------------------------------
        
        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
