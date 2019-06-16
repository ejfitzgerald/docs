pipeline {
  agent {
    docker {
      image "gcr.io/fetch-ai-images/ci-python:0.1.2"
      label "prod-jenkins-slave"
    }
  }

  stages {
    stage('Install dependencies') {
      steps {
        sh 'pipenv install'
      }
    }
    stage('Build the site') {
      steps {
        sh 'pipenv run mkdocs build'
      }
    }
    stage('Deployment') {
      // environment {
      //   GIT_USERNAME = 'fetch-bot'
      //   GIT_PASSWORD = credentials('fetchbot-token')
      // }

      when {
        branch "feature/deployment"
      }

      steps {
        sh "rm -Rf site" // remove the previously built site
        sh "mkdocs gh-deploy -b feature/deployment-test"
      }

    } // deployment stage
  } // stages
} // pipeline