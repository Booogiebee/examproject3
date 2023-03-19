pipeline {
agent any
environment {
env = "production"
}

stages {
stage('git clone') {
steps {
git branch: 'master', url: 'https://github.com/Booogiebee/microservices-demo.git'
}
}
stage('Deploy socks application') {
steps {
dir('deploy/kubernetes') {
sshagent(['SSH']){
sh "scp -o strictHostKeyChecking=no complete-demo.yaml ubuntu@44.203.236.249:/home/ubuntu"
}
script {
try{
sh "ssh ubuntu@44.203.236.249 kubectl apply -f complete-demo.yaml"
} catch(error){
sh "ssh ubuntu@44.203.236.249 kubectl create -f complete-demo.yaml"
}
}
}
}
}