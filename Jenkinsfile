pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/xuarig007/ddd-sample', credentialsId: 'git-login', branch: 'master')
      }
    }
    stage('Compile') {
      steps {
       withMaven(maven: 'maven') {
          bat 'mvn clean compile'
        }

      }
    }
    stage('Test') {
      steps {
        withMaven(maven: 'maven') {
          bat 'mvn test'
        }

      }
    }
    stage('Package') {
      steps {
       withMaven(maven: 'maven') {
          bat 'mvn package -DskipTests'
        }

      }
    }

   stage('Quality') {
      steps {
       withSonarQubeEnv('SonarQ') {
          bat 'mvn sonar:sonar -Dsonar.projectKey="xuarig_jenkins-sample"'
        }
    }
   }
 }
}
