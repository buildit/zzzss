#!groovy

def pipe(command){
    sh(script: command, returnStdout: true)
}

def getCommitTag() {
  return pipe("git tag -l --points-at HEAD")
}

node {
  stage('Setup') {
    sh 'echo *******'
    sh "echo git tag -l --points-at HEAD > tag";
    def tag=readFile('tag').trim()
    echo "tag=$tag";

    sh "curl -L https://dl.bintray.com/buildit/maven/jenkins-pipeline-libraries-${env.PIPELINE_LIBS_VERSION}.zip -o lib.zip && echo 'A' | unzip lib.zip"
    sh 'echo ${tag}'
  }

  stage('Checkout from SCM') {
    sh 'echo *******'
    sh "git tag -l --points-at HEAD"
    checkout scm
    sh 'echo *******'
    sh "git tag -l --points-at HEAD"
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
