pipeline {
  agent any
  stages {
    stage('Code') {
      steps {
        git(url: 'https://github.com/slysenko1/cicd-pipeline-train-schedule-git.git', branch: 'master', changelog: true)
      }
    }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''npm install
ng build --prod
mkdir pkgs
zip -r pkgs/${JOB_BASE_NAME}-${BUILD_NUMBER}.zip dist/'''
          }
        }
        stage('Dev') {
          steps {
            echo 'Build Development Artifact'
          }
        }
        stage('QA') {
          steps {
            echo 'Build QA Artifact'
          }
        }
        stage('STG') {
          steps {
            echo 'Build Staging'
          }
        }
        stage('PROD') {
          steps {
            echo 'Build Production'
          }
        }
      }
    }
    stage('Test') {
      steps {
        echo 'Testing'
      }
    }
    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            echo 'Deploying'
          }
        }
        stage('DEV') {
          steps {
            echo '... in development'
          }
        }
        stage('QA') {
          steps {
            echo '... in QA'
          }
        }
        stage('STG') {
          steps {
            echo '... in Staging'
          }
        }
        stage('PROD') {
          steps {
            echo '... in Production'
            input 'Do you want to deploy in Production '
          }
        }
      }
    }
  }
}