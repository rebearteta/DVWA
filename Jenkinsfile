pipeline {
    agent none
    stages {
        stage('Semgrep Scan') {
            steps {
                script {
                    // Run Semgrep using a Docker image
                    sh """
                        docker run --rm -v \$(pwd):/src returnto/semgrep:latest \
                        semgrep --config auto --json --output semgrep_results.json /src
                    """
                }
            }
        }
        stage('Compilation') {
            agent {
                docker { image 'php:8.2-cli' }
            }
            steps {
                sh 'echo "Compilando..."'
            }
        }
        stage('Build') {
            agent {
                docker { image 'php:8.2-cli' }
            }
            steps {
                sh 'echo "docker build -t my-php-app ."'
            }
        }
        stage('Deploy') {
            agent {
                docker { image 'php:8.2-cli' }
            }
            steps {
                sh 'echo "docker run my-php-app ."'
            }
        }
    }
}
