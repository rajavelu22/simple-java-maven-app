pipeline {
    agent { node { label 'NodeOne' } }

    stages {
        stage('Git-Clone') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/rajavelu22/simple-java-maven-app.git'
            }
        }
        stage('Maven-Package') {
            steps {
               sh '''
        export PATH=/opt/apache-maven-3.9.9/bin:$PATH
        mvn package
        '''
            }
        }
        stage('Junit-Test'){
            steps{
                junit testResults: 'target//surefire-reports/*.xml'
            }
        }
        stage('Archive-Artifacts'){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar'
            }
        }
    }
    post {
        success {
            mail bcc: '', 
                 body: 'The Jenkins build has successfully completed. Please review the results.', 
                 cc: '', 
                 from: '', 
                 replyTo: '', 
                 subject: 'Jenkins Build Success Notification', 
                 to: 'rajavelujansi@gmail.com'
        }
    }
}
