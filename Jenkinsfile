pipeline 
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '2e024ab6-cb3e-4e88-9651-a78810d0722d', path: '', url: 'http://172.31.32.228:8080')], contextPath: 'test1', war: '**/*.war'   
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '2e024ab6-cb3e-4e88-9651-a78810d0722d', path: '', url: 'http://172.31.36.57:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
