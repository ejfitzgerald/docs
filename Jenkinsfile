pipeline {
  agent none

  stages {
    stage('Basic Checks') {

      agent {
        docker {
          image "gcr.io/fetch-ai-images/ci-python:v1"
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
      } // stages
    } // basic check stage

    // stage('Deployment') {

    //   agent {
    //     docker {
    //       image "google/cloud-sdk:latest"
    //       label "prod-jenkins-slave"
    //     }
    //   }

    //   environment {
    //     GOOGLE_SERVICE_ACCOUNT_KEY = credentials('playground-deploy-json')
    //     GOOGLE_CI_PROJECT = 'organic-storm-201412'
    //     PYTHONUNBUFFERED = 1
    //   }

    //   when {
    //     branch "master"
    //   }

    //   steps {
    //     sh "gcloud auth activate-service-account --key-file ${GOOGLE_SERVICE_ACCOUNT_KEY}"
    //     sh "gcloud config set project ${GOOGLE_CI_PROJECT}"
    //     unstash 'frontend-build'
    //     sh 'ls -l *'
    //     sh "cd frontend && tar zxvf package.tar.gz"
    //     sh 'ls -l *'
    //     sh "cd frontend && gsutil -m rsync -r build/ gs://etch-tour.economicagents.com"
    //   }

    // } // deployment stage

  } // stages

} // pipeline