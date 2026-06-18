pipeline{
    agent any
    tools{
        maven "mymaven"
    }
    stages{
        stage('code'){
            steps{
                git cbranch: 'devops-cicd', credentialsId: 'harsha', url: 'https://github.com/jyothiharsha21/one.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Artifact'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'junit', classifier: '', file: 'target/myweb-8.7.6.war', type: 'war']], credentialsId: 'smarty', groupId: 'in.javahome', nexusUrl: '13.50.233.132:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'flm-repo', version: '8.7.6'
            }
        }
        stage('Deploy'){
            input{
                message "can I proceed with the Deployment?"
            }
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://13.61.19.102:8080')], contextPath: 'webapp', war: 'target/*.war'
            }
        }
    }
    post{
        always{
            echo "Pipeline is Success and the application is deployed"
        }
    }
}
