pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                bat 'mvn -B -DskipTests clean package' 
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('doc') {
            steps {
                bat 'mvn javadoc:javadoc --fail-never'
            }
        }
        // stage('test') {
        //     steps {
        //         bat 'mvn test --fail-never'
        //     }
        // }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/surefile-reports/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
