pipeline
{
    agent any
    stages
    {
        stage('continuousdownloads')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('continuousbuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousdeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '38bc8336-2b52-4511-ae68-75b4d539d319', path: '', url: 'http://3.108.238.20:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('continuoustesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/declarativepavan/testing.jar'
            }
        }
         stage('continuousdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '38bc8336-2b52-4511-ae68-75b4d539d319', path: '', url: 'http://172.31.38.118:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
