pipeline {

    agent any

    tools {
        maven 'Maven'
        jdk 'JDK21'
    }

    stages {

        stage('Checkout') {
            steps {
                
                git branch: 'main', url: 'https://github.com/soumadipchangder/jenkins-my-webapp'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run JUnit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'cp target/*.war /usr/local/tomcat/webapps/'
            }
        }

        stage('Start Tomcat Server') {
            steps {
                sh '/usr/local/tomcat/bin/startup.sh'
            }
        }

    }
}