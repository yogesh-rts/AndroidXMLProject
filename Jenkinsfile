pipeline {
    agent any
    environment {
        PATH="$PATH:/usr/local/bin"
        LANG="en_US.UTF-8"
        ANDROID_SDK_ROOT="/Users/yogeshkumar/Library/Android/sdk"
        ANDROID_AVD_HOME="/Users/yogeshkumar/.android/avd"
        JAVA_HOME="/opt/homebrew/opt/openjdk@17"
    }
    options {
        timeout(time:2, unit:'HOURS')
    }
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Clone repo') {
            steps {
               git branch: 'main', credentialsId: 'MyGitHub', url: 'https://github.com/yogesh-rts/AndroidXMLProject.git'
            }
        }
        stage('Build APK') {
            steps {
                script {
                  sh './gradlew assemble'
                  sh 'find . -name "*.apk" -exec cp {} . \\;'
                  sh "rename -v 's/app/Android-UI-${BUILD_NUMBER}/' app-*apk"
                  archiveArtifacts artifacts: '*.apk'
                }
            }
        }
    }
}
