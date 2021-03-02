pipeline {
  agent {
    node {
      label 'SLAVE01'
    }

  }
  stages {
    stage('Cleanup Workspace') {
      steps {
        cleanWs()
        sh """
                        echo "Cleaned Up Workspace for ${APP_NAME}"
                        """
      }
    }

    stage('Code Checkout') {
      steps {
        checkout([
                              $class: 'GitSCM', 
                              branches: [[name: '*/master']], 
                              userRemoteConfigs: [[url: 'https://github.com/RathnamSai/DevOps-Demo-WebApp.git']]
                          ])
        }
      }

      stage('Code Build') {
        steps {
          sh 'mvn install -Dmaven.test.skip=true'
        }
      }

      stage('Priting All Global Variables') {
        steps {
          sh '''
                env
                '''
        }
      }

    }
    tools {
      maven 'Maven3.6.3'
    }
    environment {
      APP_NAME = 'DCUBE_APP'
      APP_ENV = 'DEV'
    }
    options {
      buildDiscarder(logRotator(daysToKeepStr: '15', numToKeepStr: '10'))
    }
  }