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
        sh 'docker build -t app --no-cache .'
        sh 'docker tag app chandankashyap2310/nodetest'
        sh 'docker login --username=chandankashyap2310 --password=Hrhk@1234'
        sh 'docker push chandankashyap2310/nodetest'
      }
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker pull chandankashyap2310/nodetest'
        sh 'docker run -d -p 8090:8090 --name app chandankashyap2310/nodetest:latest'
        sh 'docker rmi -f app chandankashyap2310/nodetest'
      }
    }
  }
  catch (err) {
    throw err
  }
}
