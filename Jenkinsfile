pipeline{
    agent {
        label 'node2'
    }
    tools{
        maven 'maven'
    }
    stages{
        stage('build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }

        stage(deploy){
            steps{
                sh """
                sudo docker run -d --name tomcat -p 8090:8080  tomcat
                sudo docker cp $WORKSPACE/target/*.war tomcat:/usr/local/tomcat/webapps"""
            }
        }

    }
}
