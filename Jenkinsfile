pipeline{
    agent {label "agent-server"}
    stages{
        stage("Code Clone"){
            steps{
                git url:"https://github.com/AmanCloudOps/django-notes-app.git", branch:"main"
            }
        }
        
        stage("Code Build"){
            steps{
                sh "docker build -t node-app ."
            }
        }
        
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHubCred', passwordVariable: 'dockerHubPass', usernameVariable: 'dockerHubUser')]) {
                sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                sh "docker image tag node-app:latest ${dockerHubUser}/notes-application:latest"
                sh "docker push ${dockerHubUser}/notes-application:latest"
                }
                
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose down && docker compose up -d --build"
            }
        }
    }
}
