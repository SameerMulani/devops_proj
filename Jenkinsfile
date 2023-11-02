pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            steps{
                deploy adapters: [tomcat9(path: '', url: 'http://localhost:8069/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
