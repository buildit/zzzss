#!groovy

def pipe(command){
    sh(script: command, returnStdout: true)
}

def getCommitTag(commit = "HEAD") {
  return pipe("git tag -l --points-at ${commit}")
}

node {
  stage('Setup') {
    sh "git tag -l --points-at HEAD"
    sh "curl -L https://dl.bintray.com/buildit/maven/jenkins-pipeline-libraries-${env.PIPELINE_LIBS_VERSION}.zip -o lib.zip && echo 'A' | unzip lib.zip"
    tag = getCommitTag()
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
