def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
pipeline {
    agent any
    environment {
        NEXUSPASS = credentials('nexuspass')
    }

    stages {      

        stage('Setup parameters') {
            steps {
                script { 
                    properties([
                        parameters([
                            string(
                                defaultValue: '', 
                                name: 'BUILD', 
                            ),
							string(
                                defaultValue: '', 
                                name: 'TIME', 
                            )
                        ])
                    ])
                }
            }
		}

        stage('Ansible Deploy to Pord'){
            steps {
                ansiblePlaybook([
                inventory : 'ansible/prod.inventory',
                playbook : 'ansible/site.yml',
                installation: 'ansible',
                colorized: true,
                credentialsId: 'applogin-prod',
                disableHostKeyChecking: true,
                extraVars   : [
                   	USER: "admin",
                    PASS: "${NEXUSPASS}",
			        nexusip: "172.31.10.199",
			        reponame: "Aprofile-release",
			        groupid: "QA",
			        time: "${env.TIME}",
			        build: "${env.BUILD}",
                    artifactid: "aproapp",
			        vprofile_version: "aproapp-${env.BUILD}-${env.TIME}.war"

                ]
                ])
            }
        }
    }
    post {
        always {
            echo 'Slack Notificationss.'
            slackSend channel: '#jenkinscicd',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
        }
    }
}