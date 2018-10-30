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
    stage('Build Docker test'){
     sh 'docker build -t aishwarydhare/docker-react -f Dockerfile.dev .'
    }
    stage('Docker test'){
      sh 'docker run --rm react-test'
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t aishwarydhare/docker-react -f Dockerfile.dev .'
        sh 'docker run aishwarydhare/docker-react npm run test -- --coverage'
      }
    }
  }
  catch (err) {
    throw err
  }
}