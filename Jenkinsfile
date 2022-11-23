pipeline {
    agent any
  environment {
      // SEMGREP_BASELINE_REF = ""

        SEMGREP_APP_TOKEN = credentials('secret_key')
        SEMGREP_PR_ID = "${env.CHANGE_ID}"

      //  SEMGREP_TIMEOUT = "300"
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/nishanthv-hexa/VULNDep.git'
            }
            }
        
      stage('Semgrep-Scan') {
          steps {
            sh "pip3 install semgrep"
            sh "semgrep ci"
          }
      }
        stage('Dependency Check'){
            steps {
		dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Owasp dependency Check'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
 }
}
}
}
