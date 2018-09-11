pipeline {
    agent any
    stages {
        stage('Build Frontend Web') {
            steps {
                echo 'Building Frontend Angular'
                dir ('Angular6BaseCli/'){
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy Frontend Web') {
            steps {
                echo 'Deploy Frontend Angular'
                sh 'docker build -t frontIvette .'
                sh 'docker run -d -p 9092:80 frontIvette '
            }
        }
    }
    post { 
        always { 
            deleteDir()
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            sh 'docker-compose down'
            echo 'I am unstable :/'
        }
        failure {
            sh 'docker-compose down'
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}