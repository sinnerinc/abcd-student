pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('Code checkout from GitHub') {
            steps {
                script {
                    cleanWs()
                    git credentialsId: 'github-pat', url: 'https://github.com/sinnerinc/abcd-student', branch: 'main'
                }
            }
        }
		stage('[ZAP] Baseline passive-scan') {
			steps {
				sh 'osv-scanner scan --lockfile package-lock.json --format json --output osv-scan-results.json'
			}
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
					defectDojoPublisher(artifact: '${WORKSPACE}/osv-scan-results.json', 
	                   productName: 'Juice Shop', 
	                   scanType: 'OSV Scan', 
	                   engagementName: 'mknyc@sinnerinc.net')

	
				}


			}
	}

		
    }
}
