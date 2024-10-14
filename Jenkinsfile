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
/*
#			sh '''
#				docker run --name juice-shop -d --rm \\
#					-p 3000:3000 \\
#					bkimminich/juice-shop
#				sleep 5
#			'''
*/
			sh 'osv-scanner scan --lockfile package-lock.json'

/*
#			sh '''
#				docker run --name zap \\
#					--add-host=host.docker.internal:host-gateway \\
#					-v /home/sinnerinc/abcd-student/.zap:/zap/wrk/:rw \\
#					-v /home/sinnerinc/abcd-student/.zap/reports:/zap/wrk/reports:rw \\
#					-t ghcr.io/zaproxy/zaproxy:stable bash -c \\
#					"zap.sh -cmd -addonupdate; zap.sh -cmd -addoninstall communityScripts -addoninstall pscanrulesAlpha -addoninstall pscanrulesBeta -autorun /zap/wrk/passive_scan.yaml" \\
#					|| true
#
			'''
*/
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
			}
*/

		}
}

		
    }
}
