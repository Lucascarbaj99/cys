
node {
  stage('Clean Workspace'){
    cleanWs()
  }

  stage("Main build") {
    
    stage('Checkout') {
      checkout scm
    }
  
    stage ('Build') {
        bat label:
          'Running build',
        script: '''
          MSBuild /p:Configuration=Release;Platform="Any CPU" biblioSECA.sln
        '''
    }
  }
  
	stage ('Tests') {
		bat label:
			'Running tests',
        script: '''
			echo EJECUTANDO TESTS ######################################
			"C:/Program Files (x86)/TestWindow/vstest.console.exe" CapaPruebas/bin/Release/CapaPruebas.dll
			IF %ERRORLEVEL% NEQ 0 ( echo  	--^> Fallaron las pruebas de persistencia & exit %errorlevel%)
			echo TEST OK
		'''
  }
  
}