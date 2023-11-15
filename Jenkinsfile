pipeline {
  agent { label "Jenkins-Agent" }
  environment {
      APP_NMAE = "register-app-pipeline
  }
  stages {
    stage ("Claean up workspace") {
        steps {
            cleanWS()
        }
    }
    stage ("git Checkout") {
        steps {
            git branch: 'main', credentialsId: 'github', url: 'https://github.com/kumarvmadhu/gitops-register-app'
        }
    }
    stage ("Update deployment tags") {
        steps {
            sh """
             cat deployment.yaml
              sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
              cat deployment.yaml
              """
        }
    }
    stage ("Push the updated deployemnt to git") {
      steps {
          sh """
          git config --global user.name "kumarvmadhu"
          git config --global user.email "abc@gmail.com"
          git add deployment.yaml
          git commit -m "Updated Deployment Manifest"
          """
          withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
          sh "git push https://github.com/kumarvmadhu/gitops-register-app main"
         }
       }
     }
  }
