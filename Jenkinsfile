properties([pipelineTriggers([githubPush()])])

node('linux') { 
	stage('Test') {    
		git 'https://github.com/hempandey1/java-project.git'
		sh 'ant -buildfile test.xml' 
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml'   
	}  
	stage('Deploy'){
		sh 'aws s3 cp /workspace/java-pipeline/dist/*.jar s3://hemw10/'
	}
	
}
