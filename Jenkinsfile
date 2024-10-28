pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('Code checkout from GitHub') {
            steps {
                script {
                    //cleanWs()
                    git credentialsId: 'github-pat', url: 'https://github.com/sinnerinc/abcd-student', branch: 'main'
                }
            }
        }

		stage('Trufflehog scan') {
			when {
                expression {
                    return false // Change to true to enable the step
                }
            }

			steps {
				sh 'trufflehog git file://. --only-verified --json > trufflehog-scan-results.json'
				//--output trufflehog-scan-results.json
			}

			post {
				always {
						
					sh 'echo scan_done'	

					defectDojoPublisher(artifact: '${WORKSPACE}/trufflehog-scan-results.json', 
	                   productName: 'Juice Shop', 
	                   scanType: 'Trufflehog Scan', 
	                   engagementName: 'mknyc@sinnerinc.net')
				}
			}
		}

		stage('Semgrep scan') {
			when {
                expression {
                    return true // Change to true to enable the step
                }
            }

			steps {
				sh 'semgrep scan --config auto --json --json-output=semgrep-results.json'
			}

			post {
				always {
						
					sh 'echo scan_done'	

					defectDojoPublisher(artifact: '${WORKSPACE}/semgrep-results.json', 
	                   productName: 'Juice Shop', 
	                   scanType: 'Semgrep JSON Report', 
	                   engagementName: 'mknyc@sinnerinc.net')

	
				}

			}	
    	}
	}
}
