node {  
    def mvn-home = tool name: 'mvn-home', type: 'maven' 
    stage('Git-Checkout') { 
        git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/vikas99341/web-app.git' 
    }
    stage('Clean-Compile') { 
        $(mvn-home)/bin/mvn clean compile 
    }
    stage('Package') { 
        $(mvn-home)/bin/mvn package
    }
}
