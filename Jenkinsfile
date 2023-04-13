pipeline {
    agent { docker { image 'python:3.10.7-alpine' } }

    parameters {
        string(name: 'BRANCH_NAME', description: 'Enter the name of the branch to build', defaultValue: 'master')
        string(name: 'GITHUB_URL', description: 'Enter the GITHUB URL', defaultValue: 'https://github.com/shai-shabtai/MySoftware.git')
    }
    triggers {
        pollSCM '*/2 * * * *'
    }
    stages {
        stage('GitHub Checkout') {
            steps {
                    checkout([$class: 'GitSCM', branches: [[name: "${params.BRANCH_NAME}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: "${params.GITHUB_URL}"]]])

            }
        }
        stage('Execute python script') {
            steps {
                    sh "python3 main.py"
            }
        }
    }
	post {
        always {
                echo "Pipeline successfully run"
        }
    }
}