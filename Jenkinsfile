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

  // 📩 Add post section for email notifications
  post {
    success {
      emailext(
        subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """<p>Good news!</p>
                 <p>The Jenkins pipeline <b>${env.JOB_NAME}</b> build <b>#${env.BUILD_NUMBER}</b> was successful.</p>
                 <p>Check the console output: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
        to: "Baskarp31@gmail.com"
      )
    }
    failure {
      emailext(
        subject: "❌ Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """<p>Oops!</p>
                 <p>The Jenkins pipeline <b>${env.JOB_NAME}</b> build <b>#${env.BUILD_NUMBER}</b> has failed.</p>
                 <p>Check the console output: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
        to: "Baskarp31@gmail.com"
      )
    }
  }
}
