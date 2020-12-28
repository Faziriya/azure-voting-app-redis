pipeline {
    agent any

    stages {
        stage('Verfify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }   
        stage('Docker build') {
            steps {
            sh(script: 'docker images -a')
            sh(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """)
            }
        }    


       stage('Start test app') {
         steps {
            sh(script: """
               ./scripts/test_container.ps1
            """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            sh(script: """
               docker-compose down
            """)
         }
      }
        
    }
}
