pipeline {
    agent any

    stages {
        stage('Clean WorkSpace') {
            steps {
                cleanWs()
            }
        }

        stage('Prepare Environment') {
            steps {
                git branch: '$BRANCH_NAME', url: 'git@gitlab.example.com:group-name/project-name-compile.git'
            }
        }

        stage('Maven pipeline') {
            steps {
                build job: 'maven-pipeline', parameters: [[$class: 'StringParameterValue', name: 'PROJECT_WORKSPACE', value: "${env.WORKSPACE}"]]
            }
        }

        stage('Deployment pipeline') {
            steps {
                build job: 'deployment-pipeline',
                        parameters: [[$class: 'StringParameterValue', name: 'PROJECT_WORKSPACE', value: "${env.WORKSPACE}"],
                                     [$class: 'StringParameterValue', name: 'PROJECT_NAME_PRE_FILETOCONTAINER_PATH', value: "${PROJECT_NAME_PRE_FILETOCONTAINER_PATH}"],
                                     [$class: 'StringParameterValue', name: 'SERVICE_NAME_PRE', value: "${SERVICE_NAME_PRE}"],
                                     [$class: 'StringParameterValue', name: 'SERVICE_NAME_PRO', value: "${SERVICE_NAME_PRO}"],
                                     [$class: 'StringParameterValue', name: 'BRANCH_NAME', value: "${BRANCH_NAME}"],
                                     [$class: 'StringParameterValue', name: 'ARTIFACT_NAME', value: "jenkins-rest-api-client-compile-ear-1.0.0.ear"]]
            }
        }
    }
}
