pipeline {
  agent any
  environment {
    VENV = 'venv'
  }
  stages {
    stage('Checkout git') {
      steps {
        git branch: 'main', url: 'https://github.com/baskarp31/GitHubCICDJenkinsPipeline'
      }
    }
    stage('Set up the venv') {
      steps {
        sh 'python3 -m venv $VENV'
        sh '$VENV/bin/python -m pip install --upgrade pip'
        sh '$VENV/bin/pip install -r requirements.txt'
      }
    }
    stage('Run the tests') {
      steps {
        sh '$VENV/bin/python -m unittest discover -s tests'
      }
    }
  }
}
