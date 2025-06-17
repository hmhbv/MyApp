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
          sh 'docker run -d -p 27017:27017 --name mongo mongo:latest
        }
      }
    }
      stage('Run Container') {
      steps {
        script {
          sh 'docker run -d -p 8081:8081 --name mongo-express mongo-express:latest'
        }
      }
    }
    stage('Run Container') {
      steps {
        script {
          sh 'docker run -d -p 3000:80 --name myapp my-app:1.0'
        }
      }
    }
  }
}
