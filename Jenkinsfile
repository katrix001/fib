pipeline {
    agent { label 'aws'}

    parameters {
        choice (name : 'NUMBER',
        choices : [10, 20, 30, 40, 50, 60, 70, 80,90],
        description : 'Select the value for F(n) for the fibonnai seq.')
    }

    options {
        buildDescarder(logRotator(daysToKeepStr: '10', numToKeepStr: '10'))
        timeout(time: 12, unit: 'HOURS')
        tmestamps()
    }

    stages {
        stage('Make Executable') {
            steps {
                sh('chmod +x ./scripts/fib.sh')
            }
        }
        stage ('Relative path'){
            steps {
                sh("./scripts/fib.sh ${env.NUMBER}")
            }
        }
        stage('Full Path') {
            steps {
                sh("${env.WORKSPACE}/scripts/fib.sh ${env.NUMBER}")
            }
        }
        stage ('Change directory'){
            steps{
                dir("${env.WORKSPACE}/scripts/") {
                    sh("fib.sh ${env.NUMBER}")
                }
            }
        }
    }
}
