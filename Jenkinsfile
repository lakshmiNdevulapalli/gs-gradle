node {
  def myGradleContainer = docker.image('gradle:jdk8-alpine')
  myGradleContainer.pull()
  stage('prep') {
    checkout scm
  }
  stage('test') {
    myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
      withEnv(['PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin']) {
        sh 'cd complete && chmod +x && ./gradlew test'
      }
    }
  }
  stage('run') {
    myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
      withEnv(['PATH+EXTRA=/usr/sbin:/usr/bin:/sbin:/bin']) {
        sh 'cd complete && chmod +x && ./gradlew run'
      }
    }
  }
}
