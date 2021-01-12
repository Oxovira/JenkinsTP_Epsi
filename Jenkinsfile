
def pom

pipeline {
    agent any
    tools{
        maven 'maven'
        jdk 'JDK 15'
    }
    parameters {
        booleanParam(name: "Perform release?", description:'',defaultValue: false)
    }
    stages {
        stage('Initialize'){
            steps{
                sh'''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh "mvn -s D:/Program Files/maven/apache-maven-3.6.3/conf/settings.xml deploy"
            }
        }
    }
}