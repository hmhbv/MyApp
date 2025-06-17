pipeline {
  agent any

  stages {
    stage('Clone Repository') {
      steps {
        git(url: 'https://github.com/hmhbv/MyApp.git', branch: 'main')
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          sh 'docker build -t my-app:1.0 -f Dockerfile .'
        }
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
