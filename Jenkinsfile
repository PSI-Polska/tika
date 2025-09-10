pipeline {
    agent any

    options {
        disableConcurrentBuilds(abortPrevious: true)
        timeout(activity: true, time: 10, unit: 'MINUTES')
    }

    tools {
        maven 'DEFAULT'
        jdk 'JDK 8 Corretto'
    }

    parameters {
         booleanParam(name: 'RELEASE_FLAG', defaultValue: false, description: 'Release new version.')
    }

    stages {
        stage('Install') {
            steps {
                script {
                    sh "mvn -B clean install"
                }
            }
        }
        stage('Deploy') {
            when {
                expression {
                    params.RELEASE_FLAG == true
                }
            }
            steps {
                script {
                    sh "mvn -B clean deploy -P TPF"
                }
            }
        }
    }
}
