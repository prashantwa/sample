#!groovy
import groovy.json.JsonSlurperClassic

node{
	def BUILD_NUMBER = env.BUILD_NUMBER
	def RUN_ARTIFACT_DIR = "tests\${BUILD_NUMBER}"
	def SFDC_USERNAME
	
	def HUB_ORG = env.HUB_ORG_DH
	def SFDC_HOST = env.SFDC_HOST_DH
	//def JWT_KEY = env.JWT_CRED_ID_DH
	def CONSUMER_KEY = env.CONNECTED_APP_CONSUMER_KEY_DH
	
	//def toolblt = tool 'toolbelt'
	stage('Checkout'){
		checkout scm
	}
	
	stage('Authorize'){
		rc = sh returnStatus:true, script:"\'C:/Program Files/Heroku/bin/sfdx _ force:auth:jwt:grant\' --clientid ${CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile C:\'\\'Users\'\\'PrashT\'\\'SFDX_Keys\'\\'server.key --instanceurl ${SFDC_HOST} --setdefaultdevhubusername"
		if(rc != 0){
			error 'Dev hub org authorization failed'
		}
	}
}