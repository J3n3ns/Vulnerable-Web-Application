pipeline { 
    agent any 
    stages { 
        stage ('Checkout') { 
            steps { 
            checkout scm
	    } 
        } 
         
        stage('Code Quality Check via SonarQube') { 
           steps { 
               script { 
                def scannerHome = tool 'sonarqube'; 
                   withSonarQubeEnv('sonarqube') { 
                   sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWSAP -Dsonar.sources=." 
                   } 
               } 
           } 
        } 
    } 
    post { 
        always { 
            recordIssues enabledForFailure: true, tool: sonarQube() 
        } 
    } 
}
