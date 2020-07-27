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
	          //sh "docker build -t my-web ."
	          dockerImage = docker.build image + ":$BUILD_NUMBER"
	        }
	      }
	    }
	    stage('Deploy Test Server') {
	      steps{
	        script {
	          sh "ls -l"
                  sh "./deploy-test.sh ${env.BUILD_ID} ${env.image}:${env.BUILD_ID}"
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
	    stage('Testing image') {
	      steps{
	        script {
	          sh "echo 3333"
	        }
	      }
	    }
		stage('End of pipeline') {
	      steps{
	        script {
	          sh "echo 5555"
	        }
	      }
		}     
	}
}
