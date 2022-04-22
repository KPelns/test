pipeline {
    
     agent any
     stages {
             
        stage('Input') {
            steps{
              script {
                        env.USERNAME = input message: 'Please enter the username',
                                parameters: [string(defaultValue: '',
                                            description: '',
                                             name: 'Name: ')]

        }
            
               
                     input('Do you want to proceed?')
                             
    }
        }
              
         stage('Upload to AWS!') {
              steps {
                  withAWS(region:'eu-west-1',credentials:'endijs') {
                  sh 'echo "Uploading content with AWS creds"'
                  s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'second-stack.yaml', bucket:'spainisdivi')
                  }
              }
         }
     
     }
     
     post {

        success {
            echo 'LETS GOOOO'
        }


        aborted {
        withCredentials([gitUsernamePassword(credentialsId: '123', gitToolName: 'Default')]) {      
        echo "Hello, you aborted the mission ${env.USERNAME}!"
      
            
            sh '''
            git branch -D revert
            git checkout main
            git pull origin main 
            git checkout -b revert
            git revert -m 1 HEAD
            git checkout main
            git merge revert
            
 
            git push origin main
            
            '''
        }
        }
        } 
        
    
}


}
© 2022 GitHub, Inc.
Terms 
Privacy
