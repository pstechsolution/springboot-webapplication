pipeline{
    tools{
          maven 'mymaven'
    }
	agent any
      stages{
           stage('Checkout'){
	    
               steps{
		 echo 'cloning'
                 git 'https://github.com/pstechsolution/springboot-webapplication.git'
              }
          }
	stage('Compile'){
             
              steps{
                  echo 'complie the code..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
		  
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		  
              steps{
	         
                  sh 'mvn test'
              }
          
          }
        
          stage('Package'){
		  
              steps{
		  
                  sh 'mvn package'
              }
          }
	  stage('Deploy'){
      agent any
      steps{
        sh label: '', script: '''rm -rf mydockerfile
	mkdir mydockerfile
	cd mydockerfile
	cp /var/lib/jenkins/workspace/CICDpipeline/target/mavewebappdemo-1.0.0-SNAPSHOT.war .
	touch dockerfile
	cat <<EOT>> dockerfile
	From tomcat:9
	ADD mavewebappdemo-1.0.0-SNAPSHOT.war /usr/local/tomcat/webapps
	EXPOSE 8080
	CMD ["catalina.sh", "run"]
	EOT
	sudo docker build -t myimage:$BUILD_NUMBER .
	sudo docker run -itd -P myimage:$BUILD_NUMBER'''
      }
    }
         
      }
}

