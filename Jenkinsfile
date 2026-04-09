pipeline {
    agent {
        label 'docker-agent'
    }
    
    stages {
        stage("first-stage") {
            parallel {
                stage ("first-stage-parallel-1") {
                    steps {
                        sh """
                          echo "Executing first-stage-parallel-1..."
                          sleep 20
                          echo "Executing first-stage-parallel-1 Complete"
                        """
                    }
                }
                stage ("second-stage-parallel-2") {
                    steps {
                        sh """
                          echo "Executing second-stage-parallel-2..."
                          sleep 20
                          echo "Executing second-stage-parallel-2 Complete"
                        """
                    }
                }
            }
        }

        stage ("second-stage") {
            steps {
                sh """
                  echo "Executing second-stage..."
                  sleep 20
                  echo "Executing second-stage Complete"
                """
            }
        }
    }
}
