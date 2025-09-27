@Library('shared') _
pipeline {
    
    agent { label 'windows' }

    stages {
        
        stage("Cleanup") {
            steps {
                cleanWs()
            }
        }
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }
        
        stage("Code") {
            steps {
               script{
               clone(url: 'https://github.com/Anand9340/django-notes-app.git', branch: 'main')
               }
            }
        }
        stage("Build") {
            steps {
                script{
                docker_build("notes-app","latest","anandsingh93")
                }
            }
        }
        stage("Push to Dockerhub") {
            steps {
                script{
                    docker_push("notes-app","latest","anandsingh93")
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "this is deploying the code"
                bat "docker compose up -d" 
            }
        }
    }
}
