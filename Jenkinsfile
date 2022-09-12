pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo"Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://localhost:9090/')], contextPath: '/cool', war: '**/*.war'
            }
        }
    }
}
