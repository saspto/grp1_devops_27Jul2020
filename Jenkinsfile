pipeline {

  agent any

  stages {

	    stage('Cloning Git') {
	      steps {
	        git 'https://github.com/saspto/grp1_devops_27Jul2020.git'
	      }
	    }
	    stage('Building image') {
	      steps{
	        script {
	          sh "ls -l"
                 # sh "docker rm -f my-web 2>&1 "
	          sh "docker build -t my-web . "
	          sh "docker run -d -p 443:80 my-web"
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
