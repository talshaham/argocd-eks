pipeline {
    agent any 
    environment {     
      REPLICA= 10
    }

    stages {

        stage('second clone') {
            steps {
                git branch: 'main', credentialsId: 'second_pipeline_gitlab_username_password', url: 'http://172.31.19.174/tal_user/deployment'
                echo 'Hello world!' 
            }
        }
        
        stage('change number of replicas') {
            steps {
                // sh 'helm uninstall weather-app'
                sh 'yq e .appDeployment.replicas="$REPLICA" -i /home/ec2-user/agent1/workspace/pipeline-deployment/mychart/values.yaml'
            }
        }

        stage('deploy') {
            steps {
                // sh 'helm install weather-app mychart'
                sh 'helm upgrade weather-app mychart'
            }
        }        
    }
  
}
