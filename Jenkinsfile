pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
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
}
