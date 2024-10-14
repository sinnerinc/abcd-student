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
				sh 'osv-scanner scan --lockfile package-lock.json'
			}
			post {
				always {
	/*
	#				sh '''
	#					docker cp zap:/zap/wrk/reports/zap_html_report.html ${WORKSPACE}/zap_html_report.html
	#					docker cp zap:/zap/wrk/reports/zap_xml_report.xml ${WORKSPACE}/zap_xml_report.xml
	#					docker stop zap juice-shop
	#					docker rm zap 
	#				'''


	#				defectDojoPublisher(artifact: '${WORKSPACE}/zap_xml_report.xml', 
	#                   productName: 'Juice Shop', 
	#                   scanType: 'ZAP Scan', 
	#                   engagementName: 'mknyc@sinnerinc.net')

	*/
				}


			}
	}

		
    }
}
