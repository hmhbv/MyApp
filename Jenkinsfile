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

    stage('Run MongoDB') {
      steps {
        script {
          sh 'docker run -d -p 27017:27017 --name mongo mongo:latest'
        }
      }
    }

    stage('Run Mongo-Express') {
      steps {
        script {
          sh 'docker run -d --link mongo:mongo -p 8081:8081 --name mongo-express mongo-express:latest'
        }
      }
    }

    stage('Run MyApp') {
      steps {
        script {
         sh 'sleep 10 && docker run -d -p 3000:3000 --name myapp my-app:1.0'
        }
      }
    }
  }
}
