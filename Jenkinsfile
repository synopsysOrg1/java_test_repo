pipeline {
    agent any
    stages {
        stage('BlackDuckSecruityScan') {
            steps {
                script {
                    def status = security_scan product: 'blackducksca', include_diagnostics: true 
                    echo "JENKINS_HOME: ${env.JENKINS_HOME}"    
                }
            }
        }
    }
}
