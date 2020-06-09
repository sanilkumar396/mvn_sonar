pipeline {
	   agent any

	   

	   stages {
		  stage('Git Scm') {
			 steps {
				git 'https://github.com/sanilkumar396/mvn_sonar.git'
			 }
		  }

		 stage('Build') {
			steps {
				withSonarQubeEnv('sonar') {
					sh '/opt/maven/bin/mvn clean verify sonar:sonar'
				}
			}
		}
		stage("Quality Gate") {
				steps {
				  timeout(time: 1, unit: 'MINUTES') {
					waitForQualityGate abortPipeline: true
				  }
				}
			  }
			  stage("Deploy") {
				steps {
				  sh '/opt/maven/bin/mvn clean install'
				}
			  }

				
			 }
	}
