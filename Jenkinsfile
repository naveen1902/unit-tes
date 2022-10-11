pipeline {

    agent any
    stages {

        stage('Checkout Codebase'){
            steps{
  
               echo "hello world"
            }
        }

        stage('Build'){
            steps{
                sh 'rm -rf lib'
                sh 'mkdir lib'
                sh 'cd lib/ ; wget https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.7.0/junit-platform-console-standalone-1.7.0-all.jar'
                sh 'cd  src ; javac -cp "../lib/junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java'
            }
        }
        
        stage ('Server'){
  steps {
   rtServer (
   id: "jfrog",
                 url: 'http://54.178.5.96:8082//artifactory',
                 username: 'admin',
                  password: 'Polaris@123',
                  bypassProxy: true,
                   timeout: 300
                        )
         
           }
    }
            
stage('upload artifactory') {
  steps {
    rtUpload (
        serverId:"jfrog" ,
        spec: '''{
             "files": [
                     {
                      "pattern": "*.txt",
                      "target" : "polaris/"
                     }
                 ]
            }''',



      )
   }
      
      }

        stage('Test'){
            steps{
                sh 'cd src/; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class CarTest --reports-dir="reports"'
                junit 'src/reports/*-jupiter.xml'
            }
        }

        stage('Deploy'){
            steps{
                sh 'cd src/ ; java App' 
            }
        }
    }

}
