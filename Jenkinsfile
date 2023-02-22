pipeline{
    tools
	{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent any
      stages
	  {
           stage('Checkout'){
	    
               steps{
		 echo 'cloning..'
                 git 'https://github.com/lerndevops/samplejavaapp'
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
          stage('build & push docker image'){
		  
              steps{
		  
                    withDockerRegistry(credentialsId: 'DOCKER_HUB_LOGIN', url: 'https://index.docker.io/v1/') {
                    sh script: 'cd  $WORKSPACE'
                   //sh script: ' echo 'docker hub login successfull''
	            sh script: 'docker build --file Dockerfile --tag docker.io/praveenbiradar1/demoapp:$BUILD_NUMBER .'
                    sh script: 'docker push docker.io/praveenbiradar1/demoapp:$BUILD_NUMBER'
			    
              }
          }
	     
          
      }
}
}
