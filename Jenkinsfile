pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("kevlank/train-schedule")
                }
                withDockerContainer (image: 'kevlank/train-schedule') {    
                    sh 'cd /home'
                    sh 'ls -l'
                    sh 'echo $(curl localhost:8080)'
                }
            }
        }

    }
}
