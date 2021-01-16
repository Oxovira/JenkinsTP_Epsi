
def pom

pipeline {
    agent any
    tools{
        maven 'maven'
        jdk 'JDK15'
    }
    parameters {
        booleanParam(name: "Perform release?", description:'',defaultValue: false)
         booleanParam(name: "Perform sonar?", description:'',defaultValue: false)
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
                bat 'echo mvn compile'
            }
        }
        stage('Test') {
            steps {
                bat 'echo mvn test'
            }
        }
        stage('Deploy') {
            steps {
                bat 'echo mvn -s C:/Users/alban/.m2/settings.xml deploy'
            }
        }
        stage('Release'){
            when { expression {params['Perform release?']} }
                steps {
                    script
                    {
                        pom = readMavenPom file: 'pom.xml'
                    }
                    withCredentials([usernamePassword(credentialsId: '8e79fa76-9d20-45ea-8486-dbd2b99f69ca', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]){
                    bat 'git config --global user.email "alban.tipe@gmail.com"'
                    bat 'git config --global user.name "Oxovira"'
                    
                    bat 'git push origin release/'+pom.version.replace("-SNAPSHOT","")
                    bat 'mvn release:prepare -s C:/Users/alban/.m2/settings.xml -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                    bat 'mvn release:perform -s C:/Users/alban/.m2/settings.xml -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                    }
                
                }
        }
        stage('Sonar'){
            when { expression {params['Perform sonar?']} }
                steps {
                    withCredentials([usernamePassword(credentialsId: '8e79fa76-9d20-45ea-8486-dbd2b99f69ca', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]){
                        bat 'mvn -s C:/Users/alban/.m2/settings.xml sonar:sonar -Dsonar.login=admin -Dsonar.password=admin123'
                    }

                }
                
            
        }
    }
}
