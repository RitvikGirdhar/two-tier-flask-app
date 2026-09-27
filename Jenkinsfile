pipeline{
    agent {label "dev"}
    stages{
        stage("Code Clone"){
            steps{
                git url:"https://github.com/sarthujecrc/two-tier-flask-app.git",branch:"main"
            }
        }
        stage("Build"){
            steps{
                sh 'docker build -t sarthu/sarthujecrcio  .'
            }
        }
        stage("Test"){
            steps{
                echo "test cases"
            }
        }
        stage("Dockerhub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerhubme",
                    usernameVariable:"dockerhubuser",
                    passwordVariable:"dockerhubpass"
                    )]){
                sh 'docker login -u $dockerhubuser -p  $dockerhubpass'
                sh 'docker image tag sarthu/sarthujecrcio  $dockerhubuser/sarthaksinghalbest'
                sh 'docker push $dockerhubuser/sarthaksinghalbest'
                }
            }
        }
        stage("Deploy"){
            steps{
                sh 'docker compose up -d '
            }
        }
    }
}
