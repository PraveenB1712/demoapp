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
		  
         stage('Code coverage jacoco'){
		  
              steps{
		  
                 sh './gradlew clean build'
		      
		      jacoco(
                    execPattern: '**/build/jacoco/test.exec',
                    classPattern: '**/build/classes/java/main',
                    sourcePattern: '**/src/main/java'
                     )
		      
		      
                }
		 
		     post {
               always {
            // Publish the JaCoCo report
                 jacoco(
                       execPattern: '**/build/jacoco/test.exec',
                       classPattern: '**/build/classes/java/main',
                       sourcePattern: '**/src/main/java',
                       changeBuildStatus: true,
                       minimumCoverage: 80,
                       maximumComplexity: 10
                    )
                }
           }
	 }
		 
          stage('build & push docker image'){
		  
              steps{
		  
                    withDockerRegistry(credentialsId: 'DOCKER_HUB_LOGIN', url: 'https://index.docker.io/v1/') {
                    sh script: 'cd  $WORKSPACE'
                    echo 'docker hub login successfull'
	            sh script: 'docker build --file Dockerfile --tag docker.io/praveenbiradar1/demoapp:$BUILD_NUMBER .'
                    sh script: 'docker push docker.io/praveenbiradar1/demoapp:$BUILD_NUMBER'
			    
              }
          }
	     
          
      }
}
}
