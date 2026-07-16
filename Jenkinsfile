pipeline{
    agent any
    
    stages{
        stage("code push"){
            steps{
            echo "Pushing the code"
            git url:"https://github.com/ananya-porwal/django-notes-app.git", branch:"main"
            }
        }
        stage("Build "){
            steps{
                echo "Building the code "
                sh "docker build -t djangoimg1 ."
            }
            
        }
        
        stage("Push to Docker hub"){
            steps{
                echo "Pushing the image in Docker hub "
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"passworddocker", usernameVariable:"usernamedocker" )]){
                sh "docker tag djangoimg1 ${env.usernamedocker}/djangoimg1:latest"    
                sh "docker login -u ${env.usernamedocker} -p ${env.passworddocker}"
                sh "docker push ${env.usernamedocker}/djangoimg1:latest"
                }
            }
            
        }
        stage("Deploying The App"){
            steps{
                echo "Deplpying the app"
                sh "docker compose down && docker compose up -d "
            }
            
        }
    }
}
