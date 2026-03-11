pipeline {

    agent any

    tools {
        maven 'Maven'
        jdk 'JDK 25'
    }

    environment {
        TOMCAT_HOME = "/Users/soumyadip/Downloads/apache-tomcat-10.1.52"
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
                sh 'cp target/*.war $TOMCAT_HOME/webapps/'
            }
        }

        stage('Start Tomcat Server') {
            steps {
                sh '$TOMCAT_HOME/bin/startup.sh'
            }
        }

    }
}