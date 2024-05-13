pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('K8s') {
            steps {
                sh 'kubectl set image deployments/lab13-node teedyjenkins=chenyangmao/teedyjenkins:v1.0'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
