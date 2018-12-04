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
	stage ('Report'){  
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '99073a5c-1cd5-48fb-9bd4-72ef5a20d95a', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            // some block
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'         
        }
	}
