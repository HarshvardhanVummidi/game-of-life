pipeline {
    agent { label 'lt-dev'}
    triggers {
        cron('H * * * 1-5')
    }
    parameters {
        string(name:'MAVENGOAL',defaultValue:'clean package',description: 'adding parametres for the project')
    }
    stages {
        stage('scm') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'        
            }
        }
        stage('build') {
            steps {
                sh script: "mvn ${params.MAVENGOAL}"
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