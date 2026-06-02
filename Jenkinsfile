pipeline {
    agent any 
    stages {
        stage ("code cloning") {
            steps {
                echo "cloning the code from github"
                git branch: 'main', url: 'https://github.com/bhagyashree-25-sketch/django-notes-app.git'
            }
        }
        stage ("build") {
            steps {
                echo "building the code using docker file"
                sh "docker build -t my-note-app ." 
            }
        }
        stage ("pushing image to dockerhub") {
            steps {
                echo "pushing image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]) {
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag my-note-app ${env.dockerhubUser}/my-note-app:microdegree"
                sh "docker push ${env.dockerhubUser}/my-note-app:microdegree"
                }
            }
        }
        stage ("deploy to kubernetes") {
            steps {
                dir ("notesapp") {
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'kuberenetes', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                    sh "kubectl apply -f deployment.yaml"
                    sh "kubectl apply -f service.yaml"
                    }
                }
            }
        }    
    }
}    

