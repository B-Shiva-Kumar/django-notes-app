pipeline{
    agent any
    
    stages{
        stage("Github CODE clone"){
            steps{
                echo "Clone github code"
                git url: "https://github.com/B-Shiva-Kumar/django-notes-app.git", branch: "main"
            }
        }
        
        
        stage("Docker build image"){
            steps{
               echo "Build Docker image from Dockerfile" 
               sh "docker build -t noteapp ."
            }
            
        }
        
        
        stage("PUSH to Dockerhub"){
            steps{
                echo "Pushing docker image to dockerhub....."
                withCredentials([usernamePassword(credentialsId:"dockerhub_creds",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                    sh "docker tag noteapp ${env.dockerhubUser}/noteapp:latest"
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                    sh "docker push ${env.dockerhubUser}/noteapp:latest"
                }
            }
        }
        
        
        stage("Delpoy App"){
            steps{
                echo "Deploying Container...."
                sh "pwd"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}