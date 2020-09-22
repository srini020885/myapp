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
	
	stage("Quality Gate Statuc Check"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
		  if (qg.status != 'OK') {
			error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }   
	
	stage('Deploy to Tomcat'){
      
      sshagent(['root']) {
         sh 'scp -o StrictHostKeyChecking=no target/myweb-0.0.7-SNAPSHOT.war root@192.168.56.112:/opt/jenkins-app/'
      }
   }
	
}
