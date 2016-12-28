#!groovy

node {
  stage('Checkout from SCM') {
    checkout scm
  }

  stage('Validate') {
    sh 'npm run validate'
  }

  stage('Publish to npm registry') {
    sh 'echo "//registry.npmjs.org/:_authToken=${NPM_TOKEN}" > .npmrc'
    sh 'npm publish'
  }
}
