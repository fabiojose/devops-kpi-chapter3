pipeline {
  agent any

  stages {
    stage('Setup') {
      steps {
        script {
          if (env.GIT_BRANCH == 'origin/develop' || env.GIT_BRANCH ==~ /(.+)feature-(.+)/) {
            target = 'dev'
          } else if (env.GIT_BRANCH ==~ /(.+)release-(.+)/) {
            target = 'pre'
          } else if (env.GIT_BRANCH == 'origin/master') {
            target = 'pro'
          } else {
            target = 'pro'
          }

          appversion  = '1.0.0'
          version     = appversion.take(10) + '-' + env.BUILD_NUMBER
          appname     = 'http://app-ex:3000/healthcheck'
          prjname     = 'oss-opensource'

          custom = [:]
          custom['branch']      = env.GIT_BRANCH
          custom['environment'] = target
          custom['part']        = 'jenkins'
          custom['version']     = version
          custom['appname']     = appname
        }
      }
    }

    stage('Build') {
      steps {
        sh 'echo building . . .'
      }
    }

    stage('Test') {
      steps {
        sh 'echo testing . . .'
      }
    }

    stage('Deploy') {
      when {
        expression { return target == 'pro' }
      }
      steps {
        sh 'echo deploying . . .'
      }
    }
  }

  post {
    success {
      script {
        currentBuild.result = "SUCCESS"
        step([$class: 'InfluxDbPublisher', customData: custom, target: 'devops-kpi'])
      }
    }

    failure {
      script {
        currentBuild.result = "FAILURE"
        step([$class: 'InfluxDbPublisher', customData: custom, target: 'devops-kpi'])
      }
    }

    unstable {
      script {
        currentBuild.result = "FAILURE"
        step([$class: 'InfluxDbPublisher', customData: custom, target: 'devops-kpi'])
      }
    }

    aborted {
      script {
        currentBuild.result = "FAILURE"
        step([$class: 'InfluxDbPublisher', customData: custom, target: 'devops-kpi'])
      }
    }
  }
}
