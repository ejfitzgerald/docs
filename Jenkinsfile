pipeline {

  agent {
    docker {
      image "gcr.io/fetch-ai-images/ci-python:0.1.5"
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
      environment {
        FETCH_BOT_TOKEN = credentials('fetch-bot-token')
      }

      when {
        branch "feature/deployment"
      }

      steps {
        sh 'git rev-parse --short HEAD'
        sh 'pwd'
        sh "rm -Rf site" // remove the previously built site
        sh "pipenv run mkdocs -v gh-deploy -b not-gh-pages"
      }

    } // deployment stage
  } // stages
} // pipeline
