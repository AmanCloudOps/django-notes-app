@Library("shared") _
pipeline{
    agent {label "vinod"}
    stages{
        stage("hello"){
            steps{
                script{
                    hello()
                }    
            }
        }
        stage("clone"){
            steps{
                script{
                    clone("https://github.com/AmanCloudOps/django-notes-app.git","main")
                }
               
            }            
        }
        stage("build image"){
            steps{
                script{
                    docker_build("notes-app","latest","amankumar19")
                }
                
            }            
        }
        stage("push to docker hub"){
            steps{
                script{
                    docker_push("notes-app","latest","amankumar19")
                }
                
            }            
        }
        stage("deploy"){
            steps{
                sh "docker compose down && docker compose up -d"
                echo "Deploy the code"
                
            }            
        }
    }
}
