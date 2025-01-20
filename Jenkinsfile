pipeline {
    agent {
        label 'mac-agent'
    }
    environment {
        REPO_NAME = "${env.GIT_URL.tokenize('/.')[-2]}"
        FULLSCAN = "${env.BRANCH_NAME ==~ /^(main|master|develop|stage|release)$/ ? 'true' : 'false'}"
        PRSCAN = "${env.CHANGE_TARGET ==~ /^(main|master|develop|stage|release)$/ ? 'true' : 'false'}"
    }
    stages {
        stage('Polaris') {
            when {
                anyOf {
                    environment name: 'FULLSCAN', value: 'true'
                    environment name: 'PRSCAN', value: 'true'
                }
            }
            steps {
                security_scan product: 'polaris',
                    polaris_assessment_types: 'SCA',
                    polaris_application_name: "E2E-Integration-App",
                    polaris_project_name: "TestProject",
                    //polaris_branch_name: "main",
                    polaris_prComment_enabled: true
            }
        }
    }
}