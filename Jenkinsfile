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
     sh 'sudo docker build -t hamsa20/docker-react -f Dockerfile.dev .'
    }
    stage('Docker test'){
      sh 'sudo docker run -e CI=true hamsa20/docker-react npm run test'
    }    
  }
  catch (err) {
    throw err
  }
}
