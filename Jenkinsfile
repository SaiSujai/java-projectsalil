pipeline {
   environment {
     git_url = "https://github.com/SaiSujai/java-projectsalil.git"
     git_branch = "master"
   }

  agent {label 'node1'}
 
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: '119964ac-b4f6-41f1-b9ba-10f64eedc516', branch: "${git_branch}", url: "${git_url}"
       
      }
     }
    
    stage('Maven Build') {
     steps { 
          sh "mvn clean package && cp target/*.jar . "
     }
    }
     
     stage('Docker Image Build') {     
        steps {
              sh 'sudo docker build -t myjava-image . '
               }
             }
        stage('Docker image push') {
           steps {
                 withCredentials([usernamePassword(credentialsId: '76743674-809a-4b68-88f4-4168a1e9e902', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker image tag myjava-image saisujai/myjava-image:test"
                 sh "sudo docker image push saisujai/myjava-image:test" 
               } 
             }  
          }
   //   stage('Deploy app') {
   //      steps {
    //        sh 'kubectl apply -f app-deploy.yaml'
    //     }
     // }
    }

//  post {
//    always {
//      deleteDir() /* cleanup the workspace */
//    }
//  }
  }
