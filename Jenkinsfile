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
        stage('Build Docker Image'){
            script {
                app = docker.build("eskislav/train-schedule")
                app.inside {
                    sh "echo $(curl localhost:8080)"
                }
            }
        }
        stage('Push Docker Image'){
            script {
                docker.withRegistry("", "docker_account"){
                    app.push("$(env.BUILD_NUMBER)")
                    app.push("latest")
                }
            }
        }
    }
}
