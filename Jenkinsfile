pipeline {
  agent any

  stages {
    stage('Clone Repository') {
      steps {
        git(url: 'https://github.com/hmhbv/MyApp.git', branch: 'main')
      }
    }

    stage('Run with Docker Compose') {
      steps {
        script {
          sh 'docker-compose up -d --build'
        }
      }
    }
  }
}
