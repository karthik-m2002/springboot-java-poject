pipeline {   
    agent any 

    tools {
        jdk 'JDK-17'
        maven 'mvn-3.9'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/karthik-m2002/springboot-java-poject.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        
        stage('Package') {
            steps {
                sh "mvn clean package"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarq') {  
                    sh '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=sample \
                        -Dsonar.projectName="sample"
                    '''
                }
            }
        }
    }
}
