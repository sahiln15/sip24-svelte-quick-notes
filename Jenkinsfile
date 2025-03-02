pipeline {
    agent any
    tools{
        maven 'local_maven'
    }
    stages {
        stage('Build') {
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'

                }
            }
        }
        stage ('Deploy to tomcat server'){
            steps{
                deploy adapters: [deploy adapters: [tomcat9(path: '', url: 'http://localhost:9494/manager/html')], contextPath: null, war: '**/*.war']
            }
        }
    }
}