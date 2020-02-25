pipeline {
    agent {
        label 'master'
    }
    stages{
        stage ('git clone'){
            steps{
                //git  clone cmd
                git 'https://github.com/opstree/spring3hibernate.git'
            }
        }
        stage('code stability') {
         steps{
             sh ' mvn clean package'
         }   
        }
        stage('code quality') {
            steps{
                sh 'mvn findbugs:findbugs && mvn checkstyle:checkstyle'    
            }
        }
        stage('code coverage') {
            steps{
            echo "covered code"
            sh ' mvn cobertura:cobertura'
            }
        }
    }
    
    post {
        success {
            recordIssues enabledForFailure: true, tools: [checkStyle(pattern: 'target/checkstyle-result.xml')]
			recordIssues enabledForFailure: true, tools: [findBugs(pattern: 'target/findbugs.xml')]
			
		cobertura autoUpdateHealth: false,
		autoUpdateStability: false,
		coberturaReportFile: 'target/site/cobertura/coverage.xml',
		conditionalCoverageTargets: '70, 0, 0',
		lineCoverageTargets: '80, 0, 0',
		maxNumberOfBuilds: 2,
		methodCoverageTargets: '80, 0, 0',
		sourceEncoding: 'ASCII', zoomCoverageChart: false
			   
        }
    }
}
