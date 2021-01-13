
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
            steps {
                bat'''
                    echo "PATH = ${PATH}"
                    echo "MAVEN_HOME = ${MAVEN_HOME}"
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
                bat 'echo mvn test'
            }
        }
        stage('Deploy') {
            steps {
                bat 'echo mvn -s D:/Program Files/maven/apache-maven-3.6.3/conf/settings.xml deploy'
            }
        }
        stage('Release'){
            steps{
                // script{​​​​
                //     pom = readMavenPom file: 'pom.xml'
                // }
                // withCredentials([usernamePassword(credentialsId: 'oxovira', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]){​​​​
                // bat 'echo git config --global user.email "alban.tipe@gmail.com.com"'
                // bat 'echo git config --global user.name "Oxovira"'
                // bat 'echo git branch release/'+pom.version.replace("-SNAPSHOT","")
                // bat 'echo git push origin release/'+pom.version.replace("-SNAPSHOT","")
                // bat 'echo mvn release:prepare -s C:/Users/alban/.m2/settings.xml -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                // bat 'echo mvn release:perform -s C:/Users/alban/.m2/settings.xml -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                // }
            }
        }
    }
}
