#!groovy

node {
  stage('Checkout from SCM') {
    checkout(
      [
        $class: 'GitSCM',
        branches: [[name: '*/master']],
        doGenerateSubmoduleConfigurations: false, extensions: [],
        submoduleCfg: [],
        userRemoteConfigs: [[url: 'https://github.com/BillyZac/zzzss']]
      ]
    )
  }

  stage('Lint') {
    sh 'npm run lint'
  }

  stage('Publish to npm registry') {
    sh 'echo "//registry.npmjs.org/:_authToken=${NPM_TOKEN}" > .npmrc'
    sh 'npm publish'
  }
}
