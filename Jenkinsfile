pipeline {
    agent any

    tools {
        maven 'Maven'   // Jenkins Maven installation name (configure in Manage Jenkins → Tools)
        jdk 'Java21'  // Jenkins JDK installation name (Java 21, since your pom.xml requires 21)
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/MeraGithubMeriPehchan/samplejavaapp.git',
                    branch: 'master'
            }
        }

        stage('Compile') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Unit Tests & Coverage') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'   // Collect test reports
                }
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.war', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            echo "Build finished at ${new Date()}"
        }
    }
}
