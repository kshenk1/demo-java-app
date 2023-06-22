pipeline {
    agent {
        label 'gradle'
    }
 
    stages {
        stage('WinPing') {
            agent { label 'windows' }
            steps {
                powershell "mkdir C:\\this-is-a-test"
            }
        }
        stage('Build') {
            steps {
                sh "gradle build"
            }
        }
        stage('Test') {
            steps {
                sh "gradle clean test"
            }
 
            post {                
                // If Gradle was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                   publishHTML([
                      allowMissing: false, 
                      alwaysLinkToLastBuild: false, 
                      keepAll: false,
                      reportDir: '',
                      reportFiles: 'index.html', 
                      reportName: 'Serenity Report', 
                      reportTitles: '', 
                      useWrapperFileDirectly: true])
                }
            }
        }
    }
}


