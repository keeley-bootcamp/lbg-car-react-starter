pipeline {
    agent any

    environment {
        REACT_REPO = 'https://github.com/keeley-bootcamp/lbg-car-react-starter.git'
        SPRING_REPO = 'https://github.com/keeley-bootcamp/lbg-car-spring-app-starter.git'
        REACT_DIR = 'react'
        SPRING_DIR = 'spring'
        MAVEN_HOME = tool "M3"
    }

    stages {
        stage('Checkout React') {
            steps {
                dir("${REACT_DIR}") {
                    git branch: 'main', url: "${REACT_REPO}"
                }
            }
        }

        stage('Install React Dependencies') {
            steps {
                dir("${REACT_DIR}") {
                    sh "npm install"
                }
            }
        }

        stage('Test React') {
            steps {
                dir("${REACT_DIR}") {
                    sh "npm test"
                }
            }
        }

        stage('Package React') {
            steps {
                dir("${REACT_DIR}") {
                    sh "npm run build"
                }
            }
        }

        stage('Checkout Spring') {
            steps {
                dir("${SPRING_DIR}") {
                    git branch: 'main', url: "${SPRING_REPO}"
                }
            }
        }

        stage('Compile') {
            steps {
                dir("${SPRING_DIR}") {
                    sh "mvn clean compile" 
                }
            }
        }

        // not sure if we need yet
        /*stage('Install Spring Dependencies') {
            steps {
                dir("${SPRING_DIR}") {
                    sh "mvn clean install"
                }
            }
        }*/

        stage('Test Spring') {
            steps {
                dir("${SPRING_DIR}") {
                    sh "mvn test"
                }
            }
        }

        stage('Package Spring') {
            steps {
                dir("${SPRING_DIR}") {
                    sh "mvn -Dmaven.test.skip -Dmaven.compile.skip package"
                }
            }
        }
    }
}
