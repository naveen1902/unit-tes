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
                sh 'mkdir lib'
                sh 'cd var/lib/jenkins/workspace/test-pur/src/ ; wget https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.7.0/junit-platform-console-standalone-1.7.0-all.jar'
                sh 'cd  var/lib/jenkins/workspace/test-pur/src/ ; javac -cp "../lib/junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java'
            }
        }

        stage('Test'){
            steps{
                sh 'cd  var/lib/jenkins/workspace/test-pur/src/; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class CarTest --reports-dir="reports"'
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
