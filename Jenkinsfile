pipeline {
    sshagent(['AgentSSH1']) 

    parameters {
        string(name: 'WHOAMI', defaultValue: 'FahamiKareem', description: 'to capture the user')
        string(name: 'PROJECT', defaultValue: 'FinanceMe', description: 'Project Name')
    }    

    
    stages {
       
        stage('Checkout') {
            steps {        
                echo "Getting the code from Repository ${params.PROJECT} and the user is ${params.WHOAMI}"
                git 'https://github.com/fahamikareem/FinanceMe.git'
            }
        }

        stage('Agent Config') {
            steps{
                sh "scp -p StrictHostKeyChecking=No agent_config.sh"
            }
        }
    
        stage('Build') {
            steps {
                echo 'Compiling the code'
                sh 'mvn compile'
            }
        }
        stage('test') {
            steps {
                echo 'Testing the code using Maven'
                sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                echo 'Packaging - JAR'
                sh 'mvn package'
            }
        }

       
    }
}        