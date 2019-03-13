pipeline {
	
	agent any 
	environment{
		
		Docker_User = credentials('dockerhub_user')
		Docker_Password = credentials('dockerhub_pass')
		Ver = "${env.BUILD_ID}"
		Name = "${env.JOB_NAME}"
		
	}         
		stages {                 
			stage('Prepare') {                         
				steps {                                 
					echo "$Docker_User"
					sh "sudo usermod -aG docker jenkins"
				}                 
			}                 
		stage('Build') {                         
				steps {
					sh "sudo docker rmi -f front" 
					sh "sudo docker build -t front ."											               	                      
				}                 
			}                 
		stage('push') {
				steps {
					sh '''
						sudo docker login -u $Docker_User -p $Docker_Password
						sudo docker tag front felparejav/front:${Ver}
						sudo docker push felparejav/front:${Ver}
						'''
				}
			}                 
			        
		} 
} 
