pipeline {
    agent {
        label 'Linux-Build-node'
    }
    stages {
      stage('Git checkout') {
        steps {
          git branch: 'main', url: 'https://github.com/yvpatel/simple-java-maven-2025.git'
        }
      }  
      stage('compile') {
        steps {
          sh 'mvn compile'
        }
      }
      stage('test') {
        steps {
          sh 'mvn test'
        }
      }
      stage('artifact') {
        steps {
          sh 'mvn clean package'
        }
      }
      
      stage('nexus artifact upload stage') {
        steps {
          nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/myapp.war', type: '.war']], credentialsId: 'tomcatcred', groupId: 'in.ytworld', nexusUrl: '192.168.200.118:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'hotstar-repo', version: '8.3.3-SNAPSHOT'
        }
      }
      
      stage('deployment') {
        steps {
          echo 'code is deploy - actual we need to use tomcat to deploy'
          deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tom-hot', path: '', url: 'http://192.168.200.117:8080')], contextPath: 'pipeline-hotstar', war: '**/*.war'
        }
      }
    }
}
