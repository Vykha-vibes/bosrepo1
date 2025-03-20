pipeline {
  agent any
  stages {
    stage('BuildStage') {
      steps {
        git(url: 'https://github.com/Vykha-vibes/bosrepo1', branch: 'master', credentialsId: 'bea40f74-08d1-4900-9bcb-30f46ccb2fe6')
        sh '''sudo docker build -t vykha/jenkinsrepo1:ocean1 .
sudo docker push vykha/jenkinsrepo1:ocean1 .'''
      }
    }

    stage('Dev&QA') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq) || true
sudo docker run -d -p 7777:80 --name con1 vykha/jenkinsrepo1:ocean1'''
          }
        }

        stage('DeployQA') {
          steps {
            echo 'QADeploy'
          }
        }

      }
    }

  }
}