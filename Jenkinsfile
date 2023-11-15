pipeline {
  agent { label "Jenkins-Agent" }
  environment {
      APP_NMAE = "register-app-pipeline"
  }
  stages {
     stage ("Claean up workspace") {
         steps {
            cleanWS()
          }
      }
   }

}
