node()
{
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '3', daysToKeepStr: '', numToKeepStr: '3')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])

	def mavenhome = tool name: 'maven_3.8.3', type: 'maven'
	stage('CheckoutCode')
	{
		git branch: 'development', credentialsId: '8db7f7cc-fd1c-4500-a1d4-d24ab0950b32', url: 'https://github.com/abhishek-525/maven-web-application.git'
	}

	stage('Build')
	{
		sh "$mavenhome/bin/mvn clean package"
	}
	
	/*
	stage('Execute SonarQube Report')
	{
		sh "$mavenhome/bin/mvn sonar:sonar"
	}
	
	stage('Upload Artifact to Nexus')
	{
		sh "$mavenhome/bin/mvn deploy"
	}
	*/
	
	stage('Deploying application to Tomcat server')
	{
		sshagent(['9c8d8a5f-b615-4595-9f1f-27d0a8be6556'])
		{
			sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.6.89.176:/opt/apache-tomcat-9.0.58/webapps"
		}
	}
}
