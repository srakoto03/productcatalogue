pipeline {
	agent {
		label 'Linux'
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
	   stage('Publication du Binaire') {
		 steps {
		     sh "curl -u admin:formation-2021 --upload-file target/*.jar 'http://10.10.20.31:8081/repository/productcatalogue/productcatalogue${BUILD_NUMBER}.jar'"  
		 }
	   
	   }	
		
		
	}
}
