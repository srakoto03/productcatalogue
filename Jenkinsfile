pipeline {
	agent {
		label 'linux'
	}
	stages { 	 
	   stage('Test unitaires') {  
		steps { 
			 sh 'mvn test' 
		} 
	   } 
	   stage('Compilation') { 
	       steps { 
		  sh 'mvn -B -DskipTests clean package' 
	       }
	   } 
	}
}
