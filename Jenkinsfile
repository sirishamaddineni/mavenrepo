pipeline {
	agent any
	options {
		 disableConcurrentBuilds()
           }
	
	 stages{
		 stage ( 'clone' ){
		    steps{
          git "https://github.com/sirishamaddineni/mavenrepo"
          } // Checkout Source Code from GIT
		}
		stage ( 'complie' ){
		    steps{
		       withMaven( maven : 'Maven 3.5.2' ){
		       bat 'mvn clean compile'
		    } // Compiling the source code
		   }
		}
		stage ('testing' ){
		    steps{
		        withMaven( maven : 'Maven 3.5.2' ){
		        bat 'mvn test'
		       } // Testing the source code
		    }
		}
		 stage ( ' Tagging ' ){                	  
 			steps {
			       bat "git tag 'v1.1.'"
                               bat "git config user.email 'sirishamaddineni25@gmail.com'"
                               bat "git config user.name 'sirishamaddineni'"	
			}// Creating Tags 
		}
     stage( 'IQ_Scan' ){
		     steps{
			nexusPolicyEvaluation failBuildOnNetworkError: false, 
				iqApplication: 'carreer_app', 
				iqScanPatterns: [[scanPattern:  'studentapp-2.5-SNAPSHOT.war']], 
				iqStage: 'release', 
				jobCredentialsId: 'NexusIQCred'
			     
     			} // Scan the Artifacts
     		}
		 stage( "Deploy" ){
		      steps{
				nexusArtifactUploader artifacts: [[artifactId: 'studentapp-2.5-SNAPSHOT', classifier: '', file: 'C:/Program Files (x86)/Jenkins/workspace/carreerit/target/studentapp-2.5-SNAPSHOT.war', type: 'war']],
				credentialsId: '5aed14d0-99ce-4bd4-bbad-b6e3014c4e28', 
				groupId: 'maven-public', 
				nexusUrl: 'localhost:9091', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'Repo1', 
				version: '5.0'
	} // Deploying the Artifacts
     }
     
   }
}
