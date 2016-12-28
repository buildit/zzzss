#!groovy

node {
  stage('Setup') {
    sh "curl -L https://dl.bintray.com/buildit/maven/jenkins-pipeline-libraries-${env.PIPELINE_LIBS_VERSION}.zip -o lib.zip && echo 'A' | unzip lib.zip"

    git = load "lib/git.groovy"
    tag = sh(script: 'git tag -l --points-at HEAD', returnStdout: true).trim()
    sh 'echo ${tag}'
  }

  stage('Checkout from SCM') {
    checkout scm
  }

  stage('Validate') {
    sh 'npm run validate'
  }

  stage('Publish to npm registry') {
    if (tag) {
      sh 'echo "//registry.npmjs.org/:_authToken=${NPM_TOKEN}" > .npmrc'
      sh 'npm publish'
    }
  }
}
