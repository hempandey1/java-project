properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/hempandey1/java-project.git'
		sh 'ant -f test.xml -v'   
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Results') {    
		junit 'reports/result.xml'   
	}
}
