properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/hempandey1/java-project.git'
		sh 'ant -buildfile test.xml'  
		junit 'reports/results.xml'
	}   
	stage('Build') {    
		sh 'ant'   
	}   
	
}
