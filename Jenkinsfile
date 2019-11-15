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
    stage('Build'){
      if(env.BRANCH_NAME == 'master'){
        sh 'sudo docker build -t app --no-cache .'
        sh 'sudo docker tag app localhost:5000/app'
        sh 'sudo docker push localhost:5000/app'
      }
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'sudo docker pull localhost:5000/app'
        sh 'sudo docker run -d -p 8090:8090 --name app localhost:5000/app:latest'
        sh 'sudo docker rmi -f app localhost:5000/app'
      }
    }
  }
  catch (err) {
    throw err
  }
}
