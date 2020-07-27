pipeline {

  agent any

  stages {

	    stage('Cloning Git') {
	      steps {
	        git 'https://github.com/saspto/grp1_devops_27Jul2020.git'
	      }
	    }
	    stage('Build Image') {
                sh "docker build -t my-web ."
            }
	    stage('Deploy Test Server') {
	      steps{
	        script {
	          sh "ls -l"
                  sh "./deploy-test.sh ${env.BUILD_ID} my-web"
	          sh "docker build -t my-web . "
	          sh "docker run -d -p 443:8123 my-web"
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
		stage('Pushing Image') {
	      steps{
	        script {
	          sh "echo 5555"
	        }
	      }
		}     
	}
}
