pipeline {
    agent none
     environment {
                COMPONENT_NAME = 'RocketGate'
                COMPONENT_HOME = '.'
            }
    options {
        disableResume()
    }
    stages {
        stage('Build') {
            agent { label 'build' }
            steps {

               echo "Aborting all running jobs for $COMPONENT_NAME..."
               script {
                   abortAllPreviousBuildInProgress(currentBuild)
               }
               echo "Building ..."
               sh "cd $COMPONENT_HOME/.pipeline && ./npmw ci && ./npmw run build -- --pr=${CHANGE_ID}"
           }
        }
        stage('Deploy (DEV)') {
            agent { label 'deploy' }
            steps {
                echo "Deploying ..."
                sh "cd $COMPONENT_HOME/.pipeline && ./npmw ci && ./npmw run deploy -- --pr=${CHANGE_ID} --env=dev"
            }
        }
        stage('Deploy (TEST)') {
            agent { label 'deploy' }
            input {
                message "Should we continue with deployment to TEST?"
                ok "Yes!"
            }
            steps {
                echo "Deploying ..."
                sh "cd $COMPONENT_HOME/.pipeline && ./npmw ci && ./npmw run deploy -- --pr=${CHANGE_ID} --env=test"
            }
        }
        stage('Deploy (PROD)') {
            agent { label 'deploy' }
            input {
                message "Should we continue with deployment to TEST?"
                ok "Yes!"
            }
            steps {
                echo "Deploying ..."
                sh "cd $COMPONENT_HOME/.pipeline && ./npmw ci && ./npmw run deploy -- --pr=${CHANGE_ID} --env=prod"
            }
        }
    }
}