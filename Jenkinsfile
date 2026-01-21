library identifier: 'shared@main', 
        retriever: modernSCM([$class: 'GitSCMSource',
                              remote: 'https://github.com/Arbz-N/jenkins-shared-library.git'])

pipeline {
    agent { label "agent-1" }
    
    stages {
        stage("Hello"){
            steps {
                script{
                    hello()
                }
            }
        }
        
        stage('Code') {
            steps {
                echo 'Cloning the code'
                git url: "https://github.com/Arbz-N/django-notes-app.git", branch:"main"
                echo 'Code cloned successfully'    
            }
        }
        
        stage('Build') {
            steps {
                script{
                    docker_build("notes-app","latest","arbaznaeem")
                }
            }
        }
        
        stage('Push to DockerHub') {
            steps {
                script{
                    docker_push("notes-app","latest","arbaznaeem")
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo ' Deploying the application'
                sh '''
                    docker-compose down || true
                    docker-compose up -d
                    sleep 5
                    docker ps
                '''
                echo 'Application deployed successfully'
            }
        }
    }
}
