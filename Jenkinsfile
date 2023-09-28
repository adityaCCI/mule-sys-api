pipeline {
    agent any
    tools{
    maven 'Maven'
    }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                echo 'Test Application...'
                sh 'mvn test'
            }
        }
        
        stage('Deploy Cloudhub') {
            environment {
                ANYPOINT_CREDENTIALS = credentials('anypoint.creds')
            }
            steps {
                echo 'Deploying only because of code commit...'
                echo " deploying to ${params.env} environment"
                echo " worker is ${params.workerType}"
                sh "mvn clean deploy -X -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -Denvironment=Sandbox -Dworkertype=MICRO -Dworkers=1 -Dregion=us-east-2"

            }
        }
    }
}
