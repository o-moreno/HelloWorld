pipeline {
    environment {
        // Project
        projectName = 'HelloWorldDemo'
        // SonarQube
        sources='.'
        projectKey="HelloWorldDemo"
        scannerHome = tool "${env.SONARQUBE_SCANNER}"
    }
    agent {
        label 'master'
    }
    stages {
        stage('Code Analysis') {
            steps {
                echo 'Code analysis with SonarQube started'
                withSonarQubeEnv('Sonarqube-local') {
                    script {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.branch.name=${env.BRANCH_NAME} -Dsonar.projectKey=${projectKey} -Dsonar.projectName=${projectName} -Dsonar.sources=${sources}"
                    }
                }
                echo 'Code analysis with SonarQube finished'
            }
        }
    }
    post {
        always{
            echo 'Finished. Clean Up our workspace'
            deleteDir()
        }
    }
}
