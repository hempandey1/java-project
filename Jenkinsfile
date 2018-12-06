properties([pipelineTriggers([githubPush()])])

node('linux') { 
	stage('Test') {    
		sh 'ant -buildfile test.xml' 
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml'   
	}  
	stage('Deploy'){
		sh 'aws s3 cp /workspace/java-pipeline/dist/*.jar s3://hemw10/'
	}
	stage ('Report'){  
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId:  'cf08b0d1-5611-4849-bca4-464d8c0dfbb5', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            // some block
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'         
        }
	}
	
}
