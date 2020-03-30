pipeline{
	agent any
	stages{
	 stage('Git checkout'){
	 steps{
	 git 'https://github.com/ijazm123/book.git'
	  }
	}
 stage('compile'){
	 steps{
             sh "mvn compile"
	  }
	}
	stage('Code Review'){
		steps{
             sh "mvn pmd:pmd"
             }
           }
         stage('Publish PMD'){
		 steps{
		    pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
          }} 
stage('Code Testing'){
    steps{
        sh "mvn test"
             }
           }
       

stage('packaging'){
   steps{
       sh "mvn package"
    }
   }
stage('Docker Image Build'){
  steps{
    sh label: '', script: '''cp /var/lib/jenkins/workspace/book/target/addressbook.war .
sudo docker build . -t ijazm/addressbook:$BUILD_NUMBER
sudo docker push balucc/addressbook:$BUILD_NUMBER
'''
     }
  }
 }
}
