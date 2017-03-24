#!groovy
import groovy.json.JsonSlurperClassic

node{
	def BUILD_NUMBER = env.BUILD_NUMBER
	def RUN_ARTIFACT_DIR = "tests\${BUILD_NUMBER}"
	def SFDC_USERNAME
	
	def HUB_ORG = env.HUB_ORG_DH
	def SFDC_HOST = env.SFDC_HOST_DH
	def JWT_KEY = env.JWT_CRED_ID_DH
	def CONSUMER_KEY = env.CONNECTED_APP_CONSUMER_KEY_DH
	
	def toolblt = tool 'toolbelt'
	stage('Checkout'){
		checkout scm
	}
	
	withCredentials([file(credentialsId: JWT_KEY, variable: 'key_file')]) {
        stage('Create Scratch Org') {
            rc = sh returnStatus: true, script: "\'${toolbelt}/\'sfdx _ force:auth:jwt:grant --clientid ${CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile C:\'\\'Users\'\\'PrashT\'\\'.jenkins\'\\'workspace\'\\'sample_master-Y7IQ7V3ZIFXYK3O5MNLPLLNBEMHKT75LN3IAKZIFPARHOJNNBORA@tmp\'\\'secretFiles\'\\'fe93bb5d-213b-4519-8487-ab3654ec67d6\'\\'sfdcserver.key --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
            if (rc != 0) { error 'hub org authorization failed' }
	}
	
	stage('Authorize'){
		rc = sh returnStatus:true, script:"\'${toolblt}'/sfdx _ force:auth:jwt:grant --clientid \'3MVG9YDQS5WtC11pWi_GyYnepWRkE5ksP1pQSaX.HxQtZbrwGGLuGJXiKfgFtlXsKTR4.eAubAB33.47sd9_p\' --username ${HUB_ORG} --jwtkeyfile C:\'\\'Users\'\\'PrashT\'\\'SFDX_Keys\'\\'sfdxkey.key --instanceurl ${SFDC_HOST} --setdefaultdevhubusername"
		if(rc != 0){
			error 'Dev hub org authorization failed'
		}
	}
}