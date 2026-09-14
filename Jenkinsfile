@Library("Shared") _
pipeline{
    agent any
    
    stages {
        stage("Greeting test for the Shared Library.") {
            steps {
                script {
                    Hello()
                }
            }
        }

        stage("Code"){
            steps{
                script{
                    clone("https://github.com/Sunil-Phuyal/django-notes-app","main")
                }
            }
        }
        stage("Build"){
            steps{
                script{
                    docker_build("notes-app","latest","sunil714")
                }
            }
        }

        stage("Trivy Scan"){
    steps{
        sh 'trivy image --exit-code 0 --severity HIGH,CRITICAL sunil714/notes-app:latest'
    }
}
        stage("Test"){
            steps{
                 echo "This is step for testing the code"
            }
        }
        stage("Push to docker hub"){
            steps{
              script{
                  docker_push("notes-app","latest","sunil714")
              }
            }
        }
        stage("Deploy"){
            steps{
                 echo "This is step for deploying the code"
                // sh 'docker compose down'
                 sh 'docker compose pull django_app'
                 sh 'docker compose up -d --build'
            }
        }
    }
}
