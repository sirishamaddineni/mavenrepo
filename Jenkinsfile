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
     stage( "Deploy" ){
		      steps{
				nexusArtifactUploader artifacts: [[artifactId: 'gameoflife-core', classifier: '', file: 'target/studentapp-2.5-SNAPSHOT.war', type: 'war']],
				credentialsId: '5aed14d0-99ce-4bd4-bbad-b6e3014c4e28', 
				groupId: 'maven-public', 
				nexusUrl: 'localhost:9091', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'Repo1', 
				version: '4.0'
			}
     }
   }
}
