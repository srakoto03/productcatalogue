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
	            sh "curl -u admin:formation-2021 --upload-file target/productcatalogue-0.0.1-SNAPSHOT.jar 'http://10.10.20.31:8081/repository/productcatalogue/productcatalogue-0.0.1-SNAPSHOT.jar'"  
		 }	   
	   }			
	   stage('Téléchargement du binaire') { 
                steps { 
                    sh "wget -P /home/jenkins/tomcat/webapps http://10.10.20.31:8081/repository/productcatalogue/productcatalogue-0.0.1-SNAPSHOT.jar" 
                } 
          } 	
	  stage ('Test de performance avec SonaQube'){
		steps {
		      withSonarQubeEnv('SonarQube') {			        
			sh 'mvn clean verify sonar:sonar'
		      }
		}	
	 }
         stage ('Validation de l\'application') {  
                steps { 
                    sh "curl -u admin:formation-2021 --upload-file /home/jenkins/tomcat/webapps/productcatalogue-0.0.1-SNAPSHOT.jar 'http://{10.10.20.31}:8081/repository/productcatalogue/productcatalogue.jar'" 
                } 
         } 
	 stage ('Création de l\'image Docker'){
		 steps {
			 sh " wget -P /home/jenkins/tomcat/webapps http://10.10.20.31:8081/repository/productcatalogue/productcatalogue-0.0.1-SNAPSHOT.jar"
			 sh " mv /home/jenkins/tomcat/webapps/productcatalogue-0.0.1-SNAPSHOT.jar ./target/ "
			 sh " sudo docker build -t sdocker03/productcatalogue:v1 . "
			 
			
		 }
	 }
     }
}
