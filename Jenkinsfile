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
                sh 'docker build -t sarthu/sarthaksinghalbest .'
            }
        }
        stage("Test"){
            steps{
                echo "test cases"
            }
        }
        stage("Docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerhubcredu",
                    usernameVariable:"dockerhubuser",
                    passwordVariable:"dockerhubpass"
                    )]){
                sh 'docker login -u $dockerhubuser -p  $dockerhubpass'
                sh 'docker image tag sarthu/sarthaksinghalbest $dockerhubuser/sarthakhubnio'
                sh 'docker push $dockerhubuser/sarthakhubnio'
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
