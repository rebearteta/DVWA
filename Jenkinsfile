pipeline {
    agent none
    environment {
        // Define Semgrep token as a Jenkins credential
        SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN') 
        // Optional: For diff-aware scans in PRs/MRs
        // SEMGREP_BASELINE_REF = "origin/main" 
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rebearteta/DVWA'
            }
        }
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
