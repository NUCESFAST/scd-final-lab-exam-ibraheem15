pipeline {
  agent any

  stages {
    stage('21i-1102 Checkout Code') {
      steps {
        git 'https://github.com/NUCESFAST/scd-final-lab-exam-ibraheem15.git'
      }
    }

    stage('21i-1102 Install Dependencies and Build Docker Images') {
      steps {
        script {
          def services = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
          for (service in services) {
            dir(service) {
              sh 'npm --version'
              sh 'npm install'
              sh 'docker build -t your-dockerhub-username/${service} .' 
            }
          }
        }
      }
    }

    stage('21i-1102 Push Docker Images') {
      steps {
        script {
          def services = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
          docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            for (service in services) {
              docker.image("your-dockerhub-username/${service}").push("latest")
            }
          }
        }
      }
    }
  }
}