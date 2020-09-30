pipeline {
    environment {
        // Project
        projectName = 'GitHub-webhook-demo'
        // SonarQube
        sources='.'
        projectKey="GitHub-webhook-demo"
        scannerHome = tool "${env.SONARQUBE_SCANNER}"
    }
    agent {
        label 'master'
    }
    stages {
        stage('Code Analysis') {
            steps {
                echo 'Code analysis with SonarQube started'
                withSonarQubeEnv('sonarqube-damm') {
                    script {
                        bat "${scannerHome}/bin/sonar-scanner -Dsonar.branch.name=${env.BRANCH_NAME} -Dsonar.projectKey=${projectKey} -Dsonar.projectName=${projectName} -Dsonar.sources=${sources}"
                    }
                }
                echo 'Code analysis with SonarQube finished'
            }
        }
    }
}