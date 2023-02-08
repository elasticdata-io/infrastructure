pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        docker {
          image 'XYZ'
          label 'slave-A'
          args '-v /etc/localtime:/etc/localtime:ro'
        }

      }
      steps {
        echo '########################################## Building #########################################'
        sh 'scm-src/build.sh all-projects'
      }
    }

    stage('prepare_test') {
      agent {
        docker {
          image 'ABC'
          label 'laptop-hp'
          args '-v /home/jenkins/.ssh/:/home/jenkins/.ssh:ro -v /etc/localtime:/etc/localtime:ro'
        }

      }
      steps {
        echo '####################################### Prepare Test Environment ############################'
        sh 'scm-src/test.sh prepare'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'ABC'
          label 'laptop-hp'
          args '-v /home/jenkins/.ssh/:/home/jenkins/.ssh:ro -v /etc/localtime:/etc/localtime:ro'
        }

      }
      steps {
        echo '########################################## Testing ##########################################'
        sh 'scm-src/test.sh run'
      }
    }

  }
  options {
    skipDefaultCheckout(true)
  }
}