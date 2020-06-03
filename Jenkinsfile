pipeline {
  agent any
  stages {
    stage('Linting') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }
    stage('Build Image') {
        steps {
            withCredentials(bindings: [[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {
                sh '''
                docker build -t emjotpe/capstone_cloud_devops .
                '''
            }
        }
    }
    stage('Push Image') {
        steps {
            withCredentials(bindings: [[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {
                sh '''
                docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                docker push emjotpe/capstone_cloud_devops
                '''
            }
        }
    }
    stage('Set current kubectl context') {
        steps {
            withAWS(region: 'us-west-2', credentials: 'capstone') {
                sh '''
                kubectl config use-context arn:aws:eks:us-west-2:411233875469:cluster/capstoneproject
                '''
            }
        }
    }
    stage ('Deploy blue container'){
        steps{
            withAWS(region: 'us-west-2', credentials: 'capstone') {
               	sh '''
		kubectl apply -f ./blue-controller.json
		''' 
            }
        }
    }
    stage ('Deploy green container'){
        steps{
            withAWS(region: 'us-west-2', credentials: 'capstone') {
               	sh '''
		kubectl apply -f ./green-controller.json
		''' 
            }
        }
    }
  }
}
