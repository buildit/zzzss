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
    sh 'npm set init.author.name "Your Name"'
    sh 'npm set init.author.email "you@example.com"'
    sh 'npm set init.author.url "http://yourblog.com"'

    sh 'npm adduser'
    sh 'npm publish'
  }
}
