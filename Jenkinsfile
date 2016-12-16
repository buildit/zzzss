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
    // sh 'npmUser="billyzac"'
    // npmPassword="${env.NPM_PASSWORD}"
    // npmEmail="billyzacsmith@gmail.com"
    sh 'echo "$NPM_PASSWORD"'
  }
}
