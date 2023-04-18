pipeline {
    agent { label 'dev-agent' }
    
    stages{
        stage('code'){
            steps {
                git url: 'https://github.com/mansirawool17/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build & test'){
            steps {
                sh 'docker build . -t mansirawool/jenkins:latest'
            }
        }
         stage('login & push image'){
            steps {
                echo 'logging into docker and pushing image'
                withCredentials([usernamePassword(credentialsId:'dockerhub', usernameVariable:'USERNAME', passwordVariable:'PASSWORD')])
                {
                    sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
                    sh "docker push mansirawool/jenkins:latest"
                }
            }
        }
        stage('deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
