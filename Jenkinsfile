pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'dd5e2d55-289b-4e05-adac-1648088ca888', path: '', url: 'http://172.31.19.199:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/MultiBranchPipeline_Loans/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'dd5e2d55-289b-4e05-adac-1648088ca888', path: '', url: 'http://172.31.19.67:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
