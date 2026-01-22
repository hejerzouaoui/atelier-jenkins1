pipeline {
    agent any
    
    tools {
        maven 'Maven-3.9'
        jdk 'JDK-11'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo '📥 Récupération du code source...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo '🔨 Compilation du projet...'
                bat 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                echo '🧪 Exécution des tests...'
                bat 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Package') {
            steps {
                echo '📦 Packaging de l\'application...'
                bat 'mvn package -DskipTests'
            }
        }
        
        stage('Archive') {
            steps {
                echo '💾 Archivage des artifacts...'
                archiveArtifacts artifacts: '**/target/*.jar', 
                                 fingerprint: true
            }
        }
    }
    
    post {
        success {
            echo '✅ Build réussi !'
        }
        failure {
            echo '❌ Build échoué !'
        }
        always {
            echo '🧹 Nettoyage...'
        }
    }
}