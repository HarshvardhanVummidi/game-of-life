pipeline {
    agent { label 'lt-dev'}
    options {
        timeout(time: 15, unit: 'MINUTES')
    }
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
                stash name: 'warfile', includes: 'gameoflife-web/target/*.war'

            }
        }

        stage('copy to other node') {
            agent {label 'devops'}
            steps {
                unstash name: 'warfile'
            }
        }
    }
}