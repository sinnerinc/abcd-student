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
                    return true // Change to true to enable the step
                }
            }

			steps {
				sh 'trufflehog git file://. --only-verified --json '
				//--output trufflehog-scan-results.json
			}

			// steps {
			// 	sh 'osv-scanner scan --lockfile package-lock.json --format json --output osv-scan-results.json'
			// }


			post {
				always {
						
					sh 'echo scan_done'	
	/*
	#				sh '''
	#					docker cp zap:/zap/wrk/reports/zap_html_report.html ${WORKSPACE}/zap_html_report.html
	#					docker cp zap:/zap/wrk/reports/zap_xml_report.xml ${WORKSPACE}/zap_xml_report.xml
	#					docker stop zap juice-shop
	#					docker rm zap 
	#				'''

*/
					defectDojoPublisher(artifact: '${WORKSPACE}/trufflehog-scan-results.json', 
	                   productName: 'Juice Shop', 
	                   scanType: 'Trufflehog Scan', 
	                   engagementName: 'mknyc@sinnerinc.net')

	
				}


			}
	}

		
    }
}
