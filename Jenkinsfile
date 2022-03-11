pipeline {
    agent any
    tools {
  maven 'maven'
}
    stages {
        stage('Checkout'){
            steps{
                git branch: 'release', credentialsId: 'git-cred', url: 'https://github.com/Tavisca-Tanmay-Prabhudesai/java-db-Login.git'
            }
        }
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn clean package"
                // To run Maven on a Windows agent, use
                // bat "mvn  clean package"
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    deploy adapters: [tomcat8(credentialsId: 'tomcat-cred', path: '', url: 'http://172.31.85.49:8080')], contextPath: 'login', war: '**/*.war*'
                }
            }
        }
    }
}
