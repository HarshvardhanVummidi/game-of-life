pipeline {
    agent {label 'lt-dev'}
    triggers {
        cron('H * * * 1-5')
    }
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'
            }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('post build') {
            steps {
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archiveArtifacts 'gameoflife-web/target/*.war'

            }
        }
    }
}