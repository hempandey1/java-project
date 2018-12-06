properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {  
		git 'https://github.com/hempandey1/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml' 
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	
	stage('Deploy'){
		sh 'aws s3 cp /workspace/my-java-pipeline-assignment/dist/*.jar s3://hemw10/'
	}
	stage('Results') {    
		junit 'reports/result.xml'   
	} 
	
}
