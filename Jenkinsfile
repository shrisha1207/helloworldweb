pipeline { 
    agent none 
    stages {
        stage('SCM_Chekout') {
            agent {label 'master'} 
            steps { 
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/ganeshhp/helloworldweb.git']]])
            }
        }
        stage('Build'){
            agent {label 'master'}
            steps {
                sh 'mvn -f pom.xml clean package' 
            }
        }
        stage('download from github') {
            agent {label 'master'}
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/ganeshhp/helloworldweb.git']]])
            }
        }
        stage('Deploy') {
            agent {label 'master'}
            steps {
                sh 'cp target/*.war /opt/tomcat/webapps/'
                sh 'sudo nohup /opt/tomcat/bin/startup.sh'

            }
        }
    }
}
