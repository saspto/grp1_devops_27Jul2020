pipeline {
   environment {
    image = "sasdevs/my-image"
    registryCredential = "docker-hub"
    //slackChannelTest = credentials('slack-test')
    dockerImage = ''
  }

  agent any
 
  stages {
	    stage('Cloning Git') {
	      steps {
	        git 'https://github.com/saspto/grp1_devops_27Jul2020.git'
	      }
	    }
	    stage('Build Image') {
	      steps{
	        script {
                  dockerImage = docker.build image + ":$BUILD_NUMBER"
	        }
	      }
	    }
	    stage('Deploy Test Server') {
	      steps{
	        script {
	          sh "./deploy-test.sh ${env.BUILD_ID} ${env.image}:${env.BUILD_ID}"
	        }
	      }
	    }
	    stage('Testing image') {
	      steps{
	        script {
	          env.TEST = sh(returnStdout: true, script: "./test-8123.sh ${env.BUILD_ID} ${env.image}:${env.BUILD_ID}").trim()
				if (env.TEST != "SUCCESS") {
				currentBuild.result = 'ABORTED'
				error("Test Failed Aborting.. ${env.TEST}")
				// sh "curl -X POST -H 'Content-type: application/json' --data '{\"text\":\"July 27 Build ${env.BUILD_ID} Failed!\"}' ${env.slackChannelTest}"
				}else{
				// sh "curl -X POST -H 'Content-type: application/json' --data '{\"text\":\"Build ${env.BUILD_ID} Succeeded!\"}' ${env.slackChannelTest}"
				}

			}
		  }
		}
		stage('Pushing Image') {
			steps{    
				script {
					docker.withRegistry( '', registryCredential ) {
					dockerImage.push()
					}
				}
			}
		} 
		stage('Deploy Image') {
			steps{    
				script {
					sh "./deploy.sh sasdevs/my-image:${env.BUILD_ID} ${env.BUILD_ID}"
					currentBuild.result = 'SUCCESS'
				}
			}
		} 

	}
}

