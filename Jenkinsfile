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
    stage('Create Network') {
       steps {
           sh 'docker network create myapp-network'
       }
   }
    stage('Run MongoDB') {
      steps {
        script {
          sh 'docker run -d -p 27017:27017 --network myapp-network --name mongo mongo:latest'
        }
      }
    }

    stage('Run Mongo-Express') {
      steps {
        script {
          sh 'docker run -d --link mongo:mongo -p 8081:8081 --network myapp-network --name mongo-express mongo-express:latest'
        }
      }
    }

    stage('Run MyApp') {
      steps {
        script {
         sh 'sleep 10 && docker run -d -p 3000:3000 --network myapp-network --name myapp my-app:1.0'
        }
      }
    }
  }
}
