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
        stage('BuildDockerImage'){
            steps {
                sh "docker build -t eskislav/train-schedule ."
            }
        }
        stage('PushDockerImage'){
            steps {
                sh "docker push eskislav/train-schedule"
            }
        }
    }
}
