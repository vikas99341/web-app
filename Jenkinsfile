node {  
    def mvnhome = tool name: 'mvn-home', type: 'maven' 
    stage('Git-Checkout') { 
        git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/vikas99341/web-app.git' 
    }
    stage('Clean-Compile') { 
        sh "${mvnhome}/bin/mvn clean compile" 
    }
    stage('Package') { 
        sh "${mvnhome}/bin/mvn package"
    }
    stage('Sonar-Analysis') { 
		withSonarQubeEnv(credentialsId: 'sonar-cred') {
			sh "${mvnhome}/bin/mvn sonar:sonar"
			}
    }
	stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      } 
    stage('Tomcat-Deployment') { 
		sshagent(['ec2-user']) {
			sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.82.119:/opt/tomcat/webapps/'
		}
    }
}
