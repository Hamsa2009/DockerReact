node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Build Docker'){
     sh 'docker build -t hamsa20/docker-react -f Dockerfile.dev .'
    }
    stage('Docker test'){
      sh 'docker run -e CI=true hamsa20/docker-react npm run test'
    }
    stage('push image'){
        steps{
            withCredentials([usernamePassword(credentialsId: 'ACR', passwordVariable: 'password', usernameVariable: 'username')]) {
            sh 'docker login -u ${username} -p ${password} jenkinshamsa.azurecr.io'
            sh 'docker push jenkinshamsa.azurecr.io/docker-react'
            }
        }
    }
  }
  catch (err) {
    throw err
  }
}
