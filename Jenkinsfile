/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'maven:3.9.6-eclipse-temurin-17-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello Jenkins Java"'
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
            echo 'post - this will always run'
        }
        success {
            echo 'post - successful'
        }
        failure {
            echo 'post - failed'
        }
        unstable {
            echo 'post - This will run only if the run was marked as unstable'
        }
        changed {
            echo 'post - This will run only if the state of the Pipeline has changed'
            echo 'post - For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

