pipeline 
{
 agent {
       label 'appworker'
       }    
    stages 
      {
        stage('BuildandPush') 
          {
            steps {
             sh '''
                cd vote
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 183295430674.dkr.ecr.us-east-1.amazonaws.com
                docker build -t 183295430674.dkr.ecr.us-east-1.amazonaws.com/voteapp-614:vote-v${BUILD_NUMBER} .
                docker push 183295430674.dkr.ecr.us-east-1.amazonaws.com/voteapp-614:vote-v${BUILD_NUMBER}
             '''
                  }
          }
       stage('Deploy') 
          {
            steps {
             sh'''
                   docker run -p 80:80 -itd 183295430674.dkr.ecr.us-east-1.amazonaws.com/voteapp-614:vote-v5
             '''
                  }
          }
      }
}
