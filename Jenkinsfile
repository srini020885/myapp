node {
	stage('SCM checkout'){
         git 'https://github.com/srini020885/myapp'	
	}
	
	stage('compile-package'){
        def mvnHome=tool name: 'maven-3', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
        
	
	stage('SonarQube-Ananlysis'){
	def mvnHome=tool name: 'maven-3', type: 'maven'
	withSonarQubeEnv('jenkins-pipeline') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
	}
	
}
