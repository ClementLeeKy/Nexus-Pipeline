node {
      checkout scm
      
      //Pre-Condition -> Nexus Platform is hosted @ host.docker.internal:8081
      //              -> Signed into admin account, Username -> admin, Password -> Clement
      //              -> Hosted Docker Registry is created @ port host.docker.internal:8083
      //              -> Docker IP Address @ 10.11.7.47
      
      stage ('Docker Login to sync with Nexus Repository') {
            bat 'docker login -u admin -p Clement 10.11.7.47:8083'
      }
   
      stage ('Build Docker Image') {
            bat 'docker build -t docker-csv .' 
      }
      
      stage ('Tag and Push Docker Image') {
            bat 'docker tag docker-csv 10.11.7.47:8083/docker-csv'
            bat 'docker push 10.11.7.47:8083/docker-csv'
      }
      
      stage ('Pull Docker Image from Local Registry') {
            bat 'docker pull 10.11.7.47:8083/docker-csv'
      }
     
      stage ('Insert Source Code as Volume into Container') {
            bat 'docker run --name source-container -d -v /c/Users/z0048yrk/Desktop/Source-Code:/root 10.11.7.47:8083/docker-csv tail -f /dev/null'
            bat 'docker exec --interactive source-container bash -c "cd root && python test.py > output.csv"'   //output.csv file resides in Source-Code directory
       }
      
      stage ('Copy output.csv into desired directory') {
            dir("C:\\Users\\z0048yrk\\Desktop\\new-demo") {
            bat 'docker cp source-container:/root/output.csv output.csv'
      }
   }      
      stage('Stopping the Docker Container') {
            bat 'docker stop source-container'
      }
}
