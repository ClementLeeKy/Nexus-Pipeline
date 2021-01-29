node {
      checkout scm
      
      stage ('Create Docker Registry') {
            bat 'docker run -d -p 5000:5000 --restart=always --name registry registry:2'
      }
      
      stage ('Build Docker Image') {
            def image = docker.build("docker-csv", '.') 
      }
      
      stage ('Tag and Push Docker Image') {
            bat 'docker tag docker-csv localhost:5000/docker-csv'
            bat 'docker push localhost:5000/docker-csv'
      }
      
      stage ('Pull Docker Image from Local Registry') {
            bat 'docker pull localhost:5000/docker-csv'
      }
     
      stage ('Insert Source Code as Volume into Container') {
            bat 'docker run --name source-container -d -v /c/Users/z0048yrk/Desktop/Source-Code:/root localhost:5000/docker-csv tail -f /dev/null'
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
