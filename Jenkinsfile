pipeline {
  agent {
    dockerfile {
      filename 'Dokerfile'
    }

  }
  stages {
    stage('Clone Repository') {
      steps {
        git(url: 'https://github.com/hmhbv/MyApp.git', branch: 'main')
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          sh 'docker build -t my-app:1.0 .'
        }

      }
    }

    stage('Run Container') {
      steps {
        script {
          sh 'docker run -d -p 8080:80 --name myapp-container my-app:1.0'
        }

      }
    }

  }
}