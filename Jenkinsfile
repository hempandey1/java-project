properties([pipelineTriggers([githubPush()])])

node('linux') { 
	stage('Unit Tests') { 
		git 'https://github.com/hempandey1/java-project.git'
		sh 'ant -f test.xml -v' 
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}  
	stage('Deploy'){
		sh 'aws s3 cp /workspace/java-pipeline/dist/*.jar s3://hemw10/'
	}
	stage ('Report'){  
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId:   '14cd79de-ca76-4034-987f-24ff03d18292', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            // some block
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'         
        }
	}
	
}
