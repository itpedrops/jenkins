node ("ubuntu-slave") {

   stage("Clone Repository") {
        //Get some code from a GitHub repository
        git "https://github.com/itpedrops/spring-petclinic.git"
    
   }
   stage("Build Maven Image") {
        docker.build("maven-build") }
   
   stage("Remove Maven Container") {
       
        //Remove maven-build-container if it exisits
        sh "docker rm -f maven-build-container || exit 0"
   }
   stage("Run maven Container"){
        //Run maven image
        sh "docker run --rm --name maven-build-container maven-build"
   } 
   
   stage("Deploy Spring Boot Application") {
        
         //Remove maven-build-container if it exisits
        sh "docker rm -f java-deploy-container || exit 0"
       
        sh "docker run --name java-deploy-container --volumes-from maven-build-container -d -p 8081:8081 pedrops/petclinic-deploy"
   }

}
