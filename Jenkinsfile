
def pom

pipeline {
    agent any
    tools{
        maven 'maven'
        jdk 'JDK15'
    }
    parameters {
        booleanParam(name: "Perform release?", description:'',defaultValue: false)
    }
    stages {
        stage('Initialize'){
            steps{
                bat'''
                    echo "PATH = ${PATH}"
                    echo "MAVEN_HOME = ${MAVEN_HOME}"
                '''
            }
        }
        stage('Build') {
            steps {
                bat 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                bat 'mvn -s D:/Program Files/maven/apache-maven-3.6.3/conf/settings.xml deploy'
            }
        }
    }
}
