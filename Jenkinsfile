pipeline {
	agent any
	options {
		 disableConcurrentBuilds()
           }
	
	 stages{
		 stage ( 'clone' ){
		    steps{
          git "https://github.com/sirishamaddineni/mavenrepo"
          }
		}
		stage ( 'complie' ){
		    steps{
		       withMaven( maven : 'Maven 3.5.2' ){
		       bat 'mvn clean compile'
		    }
		   }
		}
		stage ('testing' ){
		    steps{
		        withMaven( maven : 'Maven 3.5.2' ){
		        bat 'mvn test'
		       }
		    }
		}
     stage( 'IQ_Scan' ){
		     steps{
			nexusPolicyEvaluation failBuildOnNetworkError: false, 
				iqApplication: 'carreer_app', 
				iqScanPatterns: [[scanPattern:  'studentapp-2.5-SNAPSHOT.war']], 
				iqStage: 'release', 
				jobCredentialsId: 'NexusIQCred'
			     
     			}
     		}
     
   }
}
