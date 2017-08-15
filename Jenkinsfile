node('master') {

	def MVNHOME = tool 'Maven3'
	
stage ('checkout code'){
	checkout scm
}
	
stage ('build'){
	sh "${MVNHOME}/bin/mvn clean install"
}

	
stage ('Test Cases Execution'){
	sh "${MVNHOME}/bin/mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
}
	
stage ('Archive Artifacts'){
	archiveArtifacts artifacts: 'target/*.war'
}

input message: "QA Team Approval for Production Deployment?"

stage ('Production Deployment'){
	sh 'cp target/*.war /opt/apache-tomcat-8.5.16/webapps'
}
	
}
