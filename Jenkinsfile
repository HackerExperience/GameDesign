#!/usr/bin/env groovy

node('!master') {

  stage('Checkout') {
    checkout scm;
  }

  if (env.BRANCH_NAME == 'master') {
    lock(resource: 'wiki-gd-deployment', inversePrecedence: true) {
      stage('Deploy') {
        sh "ssh deployer deploy wiki prod --wiki-name gd"
      }
    }
    milestone()
  } else if (env.BRANCH_NAME == 'preview') {
    lock(resource: 'wiki-gdpreview-deployment', inversePrecedence: true) {
      stage('Deploy preview') {
        sh "ssh deployer deploy wiki prod --wiki-name gdpreview --branch preview"
      }
    }
    milestone()
  }
}