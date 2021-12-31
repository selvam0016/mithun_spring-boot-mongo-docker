node{
     
    stage('SCM Checkout'){
         git credentialsId: 'Git_Cred', 
                url: 'https://github.com/selvam0016/mithun_spring-boot-mongo-docker.git'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "myMaven", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    stage('docker build'){
        sh "docker build -t devopslearner16/spring-boot-mongo ."
    }
    stage('docker push'){
        withCredentials([string(credentialsId: 'Docker_Cred', variable: 'Docker_Cred')]) {
        sh "docker login -u devopslearner16 -p ${Docker_Cred}"
        }
        sh "docker push devopslearner16/spring-boot-mongo "
    }
    stage('who'){
        sh "whoami"
    }
    stage('Deploy to k8s'){
        sh 'kubectl apply -f springBootMongo.yml'
    }
}
