node('master') 
{
    stage('ContinuousDownload')
    {
        git 'https://github.com/rushi634/maven.git'             
    }
   docker.image('maven:3.8.1-adoptopenjdk-11').inside('-v /home/ubuntu/.jenkins/workspace/SCM-pipeline') {
        stage('ContiniousBuild') {
          sh 'mvn package'
        }
    }
    stage('ContinuousDeployment')
    {
sh 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.8.15:/var/lib/tomcat9/webapps/testapp.war'
    }

    stage('ContinuousTesting')
    {
        git 'https://github.com/intelliqit/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
    }
    stage('ContinuousDelivery')
    {
    
    sh 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.1.109:/var/lib/tomcat9/webapps/prodapp.war'}
}
