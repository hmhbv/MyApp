pipeline {
  agent any

  environment {
    NETWORK_NAME = 'myapp-network'
    MONGO_VOLUME = 'mongo-data'
  }

  stages {
    stage('Clone Repository') {
      steps {
        git(url: 'https://github.com/hmhbv/MyApp.git', branch: 'main')
      }
    }

    stage('Build App Image') {
      steps {
        script {
          sh 'docker build -t my-app:1.0 -f Dockerfile .'
        }
      }
    }

    stage('Create Network & Volume') {
      steps {
        script {
          sh """
            docker network create ${NETWORK_NAME} || true
            docker volume create ${MONGO_VOLUME} || true
          """
        }
      }
    }

    stage('Start MongoDB') {
      steps {
        script {
          sh """
            docker run -d \
              --name mongo \
              --network ${NETWORK_NAME} \
              -p 27017:27017 \
              -e MONGO_INITDB_ROOT_USERNAME=admin \
              -e MONGO_INITDB_ROOT_PASSWORD=password \
              -v ${MONGO_VOLUME}:/data/db \
              mongo:latest
          """
        }
      }
    }

    stage('Start Mongo Express') {
      steps {
        script {
          sh """
            docker run -d \
              --name mongo-express \
              --network ${NETWORK_NAME} \
              -p 8081:8081 \
              -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
              -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
              -e ME_CONFIG_MONGODB_SERVER=mongo \
              mongo-express:latest
          """
        }
      }
    }

    stage('Start MyApp') {
      steps {
        script {
          sh """
            sleep 5
            docker run -d \
              --name myapp \
              --network ${NETWORK_NAME} \
              -p 3000:3000 \
              -e DOCKER_COMPOSE=false \
              my-app:1.0
          """
        }
      }
    }
  }

  post {
    always {
      echo '🧹 Cleaning up containers, volumes, and network...'
      sh '''
        docker rm -f myapp mongo mongo-express || true
        docker volume rm mongo-data || true
        docker network rm myapp-network || true
      '''
    }
  }
}
