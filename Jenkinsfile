pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java21'
    }

    environment {
        SONARQUBE = 'MySonarQube'   // Jenkins SonarQube server name
    }

     stages {
    //     stage('Checkout') {
    //         steps {
    //             git url: 'https://github.com/MeraGithubMeriPehchan/samplejavaapp.git',
    //                 branch: 'master'
    //         }
    //     }

    //     stage('Compile') {
    //         steps {
    //             bat 'mvn clean compile'
    //         }
    //     }

    //     stage('Unit Tests & Coverage') {
    //         steps {
    //             bat 'mvn test'
    //         }
    //         post {
    //             always {
    //                 junit '**/target/surefire-reports/*.xml'
    //             }
    //         }
    //     }

        stage('SonarQube Code Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    bat """
                        mvn sonar:sonar ^
                          -Dsonar.projectKey=sampleapp ^
                          -Dsonar.host.url=http://localhost:9000 ^
                    """
                }
            }
        }

        // stage('Package') {
        //     steps {
        //         bat 'mvn package'
        //     }
        //     post {
        //         success {
        //             archiveArtifacts artifacts: 'target/*.war', fingerprint: true
        //         }
        //     }
        // }
    }
}
