pipeline{
    
    agent {label "dev"};
    
    stages{
        stage("code clone"){
            steps{
                git url: "https://github.com/tauseefkhorajia/two-tier-flask-app.git" , branch: "master"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("test"){
            steps{
                echo "test ho gaya"
                
            }
        }
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCred",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                    )]){
                
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app"
                
                    }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
        
    }
}
