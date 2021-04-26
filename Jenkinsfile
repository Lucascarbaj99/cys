
node {
  stage('Clean Workspace'){
    cleanWs()
  }

  stage("Main build") {
    
    stage('Checkout') {
      checkout scm
    }
	
	stage('Actualizando bibliotecas - NuGet') {
        bat '''
			echo NUGET ######################################
            C:/NuGet_5.3.0/nuget.exe restore biblioSECA.sln
        '''	
    }
	
    stage ('Build') {
        bat label:
          'Running build',
        script: '''
			echo BUIILD ######################################
			MSBuild  /verbosity:minimal /p:Configuration=Release;Platform="Any CPU" biblioSECA.sln
        '''
    }
  }
  
	stage ('Tests') {
		bat label:
			'Running tests',
        script: '''
			echo EJECUTANDO TESTS ######################################
						
			"C:/Users/Administrador/AppData/Local/Apps/OpenCover/OpenCover.Console.exe" -target:"C:/Program Files (x86)/NUnit.org/nunit-console/nunit3-console.exe" -targetargs:CapaPruebas/bin/Release/CapaPruebas.dll /noshadow 
			
		'''
	}
	
	stage ("Status change") {
		bat label:
			'Status change',
        script: '''
			>nul find "<failure>" TestResult.xml && (
				echo "FALLARON LOS TEST."
				exit 1
			)|| (
				echo "TEST EJECUTADOS CORRECTAMENTE."
			)
		'''
	}
}