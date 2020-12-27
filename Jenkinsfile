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
                sh(script:  'docker images -a')
				sh(script: """
				cd voting-app/
				docker images -a
				docker build -t jenkins-pipeline .
				docker images -a 
				cd ..
				""")
            }
        }    
    }
}
