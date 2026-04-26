pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    echo 'Node versiyonu kuruluyor...'
                    ls -la
                    node -v
                    npm -v
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    echo 'Testler...'
                    test -f build/index.html
                    npm run test
                    ls -la
                '''
            }
        }
    }
    post{
        always{
            echo 'Build ve Test tamamlandı.'
            junit 'test-results/junit.xml'
        }
    }
}

