#!groovy

node {
  stage('Checkout from SCM') {
    checkout scm
  }

  stage('Lint') {
    sh 'npm run lint'
  }

  stage('Publish to npm registry') {
    sh 'echo "//registry.npmjs.org/:_authToken=${NPM_TOKEN}" > .npmrc'
    sh 'npm publish'
  }
}
