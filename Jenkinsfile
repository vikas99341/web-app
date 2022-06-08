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
}
