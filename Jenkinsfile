node{
   stage('1st Checkout'){
     git 'https://github.com/saranya9594/my-app.git'
   }
stage('Maven Build'){

      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
 stage('SonarQube Analysis') {
	        def mvnHome =  tool name: 'maven3', type: 'maven'
	        withSonarQubeEnv('sonar') { 
	          sh "${mvnHome}/bin/mvn sonar:sonar"
   }
 }
 stage('Build Docker Image'){
   sh 'docker build -t saranya9594/mybackup .'
   }
   stage('Nexus Image Push'){
   sh "docker login -u admin -p admin123 43.204.116.184:8083"
   sh "docker tag saranya9594/mybackup 43.204.116.184:8083/saranya:1.0.0"
   sh 'docker push 43.204.116.184:8083/saranya:1.0.0'
   }
   stage('Remove Previous Container'){
	try{
		sh 'docker rm -f tomcattest'
	}catch(error){
		//  do nothing if there is an exception
	}
 
