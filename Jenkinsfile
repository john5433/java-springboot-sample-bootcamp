pipeline {
    agent {label  "agentfarm" }
    stages {
         stage('Installing Maven'){
	     steps {
		 sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
		 sh 'sudo apt-get install -y wget tree unzip maven'
	}
     }
	stage('Compiling and Running Test Cases') {
	    steps {
		  sh 'mvn clean'
		  sh 'mvn compile'
		  sh 'mvn test'
	}
      }
	stage('Creating Package') {
	    steps {
		sh 'mvn package'
	}
      }
        stage ('Install sonarqube cli') {
             steps {
                sh 'wget -O sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip'
                sh 'unzip -o -q sonar-scanner.zip'
                sh 'sudo rm -rf /opt/sonar-scanner'
                sh 'sudo mv --force sonar-scanner-4.6.2.2472-linux /opt/sonar-scanner'
                sh 'sudo sh -c \'echo "#/bin/bash \nexport PATH=\\\"$PATH:/opt/sonar-scanner/bin\\\"" > /etc/profile.d/sonar-scanner.sh''
                sh 'sonar-scanner --version'
                }
            }
        stage ('Analyzing Code Quality') {
             steps {
                sh '/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=john5433_devops-boot-camp -Dsonar.organization=johnalbertodev -Dsonar.sources=src/main/java/ -Dsonar.java.binaries=target/classes -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=98b097d36f4420d399b5ab92cccbca1d0f773eca'
               }
            }

   }
}
