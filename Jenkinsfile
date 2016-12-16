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

    sh 'echo "billyzac\n${NPM_PASSWORD}\nbillyzacsmith@gmail.com" | npm adduser'
    sh 'npm publish'
  }
}
