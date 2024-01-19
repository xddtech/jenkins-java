/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'maven:3.9.6-eclipse-temurin-17-alpine' } }
    environment {
        SYSTEM_LEVEL = 'test-env'
    }
    
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello Jenkins Java: ${SYSTEM_LEVEL}"'
                sh 'hostname'
                sh 'mvn --version'
            }
        }
        stage('deploy') {
            steps {
                timeout(time: 5, unit: 'SECONDS') {
                    retry(3) {
                        sh 'chmod -R 777 ./deploy_me.sh'
                        sh './deploy_me.sh'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'post - this will always run, all envs ---------------------------------------- '
            sh 'set'
        }
        success {
            echo 'post - pipeline successful'
        }
        failure {
            echo 'post - pipline failed'
        }
        unstable {
            echo 'post - run only if the run was marked as unstable'
        }
        changed {
            echo 'post - run only if the state of the Pipeline has changed'
        }
    }
}

