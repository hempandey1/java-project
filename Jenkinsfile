
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
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId:'a9bbc89a-f9d9-44fd-9375-e006d6a9e12f', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            // some block
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'         
        }
	}
	
}
