pipeline { 
    agent any 
    stages { 
        stage ('Checkout') { 
            steps { 
                git branch:'master', url: 'https://github.com/RawandyRosle/Vulnerable-Web-Application.git' 
            } 
        } 
         
        stage('Code Quality Check via SonarQube') { 
           steps { 
               script { 
                def scannerHome = tool 'SonarQube'; 
                   withSonarQubeEnv('SonarQube') { 
                   sh "sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=a6b97360c882ec48ae1c9d73a38d0b1c5d2f1a7b" 
                   } 
               } 
           } 
        } 
    } 
    post { 
        always { 
            recordIssues enabledForFailure: true, tool: sonarQube() 
        } 
    } 
} 
