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
         
      }
}

