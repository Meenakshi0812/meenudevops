pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven"
    }

    stages {
        stage('Gitcheckout') {
            steps {
              git credentialsId: 'git_cred', url: 'https://github.com/Meenakshi0812/meenudevops.git' 
            }
        }
        stage('build') {
            steps {
              bat 'mvn clean install'
            }
        }
        stage('codeQuality') {
            steps {
               bat 'mvn sonar:sonar'             
            }
        }
        stage('deploy') {
            steps {
             deploy adapters: [tomcat8(credentialsId: 'Tomcat_cred', path: '', url: 'http://localhost:7000/')], contextPath: 'webAppExample', war: '**/*.war'
            }
        }
    }
}
