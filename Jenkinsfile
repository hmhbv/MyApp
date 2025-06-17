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

    stage('Run Container') {
      steps {
        script {
          sh 'docker run -d -p 3000:80 --name myapp-container my-app:1.0'
          sh 'docker run -d -p 27017:27017 --name Mongo mongo:latest'
          sh 'docker run -d -p 8081:8081 --name mongo-express mongo-express:latest'
        }
      }
    }
  }
}
