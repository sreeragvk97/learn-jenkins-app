pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    ls -la
                    node --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh """
                    ls -la
                    if [ -f build/index.html ]; then
                    echo "yes"; else echo "no";
                    fi
                    npm test
                """
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}