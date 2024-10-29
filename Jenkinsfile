pipeline{
    agent{
        label "neeraj"
    }
    
    stages{
        stage("code"){
            steps{
                echo "this is cloing the code"
                git url: "https://github.com/neeraj46665/django-notes-app.git",branch:"main"
                echo "succesfully cloned the url"
            }
            
        }
        stage("build"){
            steps{
                echo "this is building the code"
                sh "docker build -t notes-app ."
            }
        }
        stage("test"){
            steps{
                echo "this is testing the code"
            }
        }
        stage("Push to Docker Hub") {
            steps {
                echo "Logging into Docker Hub and pushing the image"
                
                withCredentials([usernamePassword(credentialsId: 'dockerhubCredential', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker tag notes-app:latest $DOCKER_USERNAME/notes-app:latest
                        docker push $DOCKER_USERNAME/notes-app:latest
                    '''
                }
            }
        }
        stage("deploy"){
            steps{
                echo "this is deploying the code"
                sh "docker compose up -d"
            }
        }
        
        
    }
}
