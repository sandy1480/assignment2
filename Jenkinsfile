node{
    
    stage('SCM Checkout'){
        git 'https://github.com/techninjas4/assignment2'
    }
    
    stage('Build Docker Image'){
        sh 'sudo docker build -t techninjas4/assignment2:1.0.0 .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'dockerHubPasswrod', variable: 'dockerHubPassword')]) {
            sh "sudo docker login -u techninjas4 -p ${dockerHubPassword}"
        }
        sh 'sudo docker push techninjas4/assignment2:1.0.0'
    }
    
    //stage('Remove Old Containers'){
    //    sh 'sudo docker stop $(docker ps -f \"name=assignment2\" -q)'
    //    sh 'sudo docker rm $(docker ps -a -f \"name=assignment2\" -q)'
    //}
    
    stage('Deploy New Containers'){
        sh 'sudo docker run -d -p 3001:3001 --label "group=assignment2" --add-host assignment2:35.178.203.40 techninjas4/assignment2:1.0.0'
    }
    
    stage('List of Containers'){
        sh 'sudo docker ps'
    }
}
