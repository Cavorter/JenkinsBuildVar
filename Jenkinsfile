pipeline {
	agent {
		node {
			label ''
			customWorkspace "C:/work/${BRANCH_NAME}"
		}
	}
	options { timestamps() }

	environment{
		MAJOR_VERSION = 1
		MINOR_VERSION = 0
		HOTFIX_VERSION = 0
		VERSION_PREFIX = "${MAJOR_VERSION}.${MINOR_VERSION}.${HOTFIX_VERSION}"
		VERSION_SHA = "sha${ GIT_COMMIT.substring(0,7).toUpperCase() }"
		BUILD_NUMBER = "${env.VER_TRAAS}"
		DISPLAY_VERSION = VersionNumber( versionNumberString: "-b${BUILD_NUMBER}${VERSION_SHA}" , versionPrefix: "${VERSION_PREFIX}", worstResultForIncrement: 'NOT_BUILT' )
		PACKAGE_VERSION = VersionNumber( versionNumberString: "${BUILD_NUMBER}" , versionPrefix: "${VERSION_PREFIX}", worstResultForIncrement: 'NOT_BUILT' )
	}

	stages {
		stage('Prepare') {
			steps {
				script {
					env.VER_TRAAS = VER_TRAAS++
					currentBuild.displayName = "${DISPLAY_VERSION}"
				}
                echo "Commit: ${GIT_COMMIT}"
				echo "SHA Substring: ${VERSION_SHA}"
				echo "Date Version: ${DATE_VERSION}"
			}
		}
		stage('Build') {
			parallel {
				stage('Build 1') {
					steps {
                        echo "${PACKAGE_VERSION}"
					}
				}
				stage('Build 2') {
					steps {
                        echo "${PACKAGE_VERSION}"
                    }
				}
			}
		}
	}
}
180302090054636
180302090108786
180302090122490