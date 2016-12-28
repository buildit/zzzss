#!groovy

node {
  stage('Setup') {
    sh "curl -L https://dl.bintray.com/buildit/maven/jenkins-pipeline-libraries-${env.PIPELINE_LIBS_VERSION}.zip -o lib.zip && echo 'A' | unzip lib.zip"

    def getShell() {
        new shell()
    }

    def getCommitTag(commit = "HEAD") {
        return getShell().pipe("git tag -l --points-at ${commit}")
    }

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
