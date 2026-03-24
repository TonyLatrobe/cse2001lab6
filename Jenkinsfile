pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello from Repo A Jenkins platform! Welcome Feature 1'
            }
        }
        stage('Environment Info') {
            steps {
                sh 'env'
                sh 'ls -alh $WORKSPACE'
            }
        }
        stage('Kubernetes Test') {
            steps {
                sh 'echo "Pretending to run kubectl..."'
                sh 'echo "node1 Ready"'
                sh 'echo "node2 Ready"'
            }
        }
        stage('Dummy Build') {
            steps {
                sh 'echo "Building..."'
                sh 'sleep 2'
                echo 'Build complete'
            }
        }
        stage('Archive Output') {
            steps {
                writeFile file: 'output.txt', text: 'Pipeline ran successfully'
                archiveArtifacts artifacts: 'output.txt', fingerprint: true
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}