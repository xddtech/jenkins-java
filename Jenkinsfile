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
                        sh './deploy_me.sh'
                    }
                }
            }
        }
    }
}

