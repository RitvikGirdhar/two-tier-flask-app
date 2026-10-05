pipeline {
    agent any

    stages {

        stage("Code") {
            steps {
                git url: "https://github.com/RitvikGirdhar/two-tier-flask-app.git",
                    branch: "main"
            }
        }

        stage("Build") {
            steps {
                sh 'docker build -t sarthu/sarthaksinghal:latest .'
            }
        }

        stage("Test") {
            steps {
                echo "test cases"
            }
        }

        stage("Docker Hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "JiyaDockerHub",
                    usernameVariable: "dockerhubuser",
                    passwordVariable: "dockerhubpassword"
                )]) {

                    sh 'docker login -u "$dockerhubuser" -p "$dockerhubpassword"'

                    sh 'docker image tag sarthu/sarthaksinghal:latest "$dockerhubuser/devking:latest"'

                    sh 'docker push "$dockerhubuser/devking:latest"'
                }
            }
        }

        stage("Deploy") {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
