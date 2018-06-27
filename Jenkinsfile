pipeline {
   agent any
   tools{
       maven "maven_354"
       jdk "java_8"
   }
   stages{
   stage('Preparation') { 
      steps{
      git 'https://github.com/guillemhs/simple-maven-project-with-tests.git'
      }
   }
   stage('Build') {
      // Run the maven build
      steps{
         sh "mvn install"
     }
   }
stage('SonarQube Analysis') {
   steps {
    withSonarQubeEnv('Sonar') {
     sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -Dsonar.projectKey=com.itnove.sample -Dsonar.projectName=com.itnove.sample -Dsonar.projectVersion=${BUILD_NUMBER} -Dsonar.language=java -Dsonar.sources=src/ -Dsonar.sourcesEnconding=UTF-8 -Dsonar.java.binaries=target/classes -Dsonar.exclusions=src/test/**'
    }
   }
   stage('Results') {
       steps{
          junit '**/target/surefire-reports/TEST-*.xml'
          archiveArtifacts 'target/*.jar'
       }
   }
   }
}
}
