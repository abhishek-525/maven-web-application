pipeline
{
    agent any
	
	options 
	{
  		timestamps
	}


    tools 
    {
        maven 'maven_3.8.3'
    }


    stages
    {
        input 
        {
            message 'kkkkkkkkkkkkkkkkkkk'
        }

        stage('CheckoutCode')
        {
            steps
            {
                git branch: 'development', credentialsId: '8db7f7cc-fd1c-4500-a1d4-d24ab0950b32', url: 'https://github.com/abhishek-525/maven-web-application.git'
            }
        }

        stage('MavenBuild')
        {
            steps
            {
                sh "mvn clean package"
            }
        }

        stage('UploadArtifacttoNexus')
        {
            steps
            {
                sh "mvn deploy"
            }
        }
