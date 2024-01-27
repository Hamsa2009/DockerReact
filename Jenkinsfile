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
    stage('Push Image'){
      app = docker.build('jenkinshamsa.azurecr.io/event-service')
      docker.withRegistry('https://jenkinshamsa.azurecr.io', 'ACR'){
          app.push("${env.BUILD_NUMBER}")
          app.push('latest')
       }
    }    
  }
  catch (err) {
    throw err
  }
}
