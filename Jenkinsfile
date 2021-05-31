pipeline {
    agent any
    
    parameters {
        string(name: 'NAME', defaultValue: 'gremio-example', description: 'name image')
        string(name: 'APP', defaultValue: 'gremio-example', description: 'name image')
    }
    triggers { pollSCM('* * * * *') }
    
    
    stages {
        stage('download git repo'){

    steps {
        git branch: 'master', url: 'https://github.com/blocer-vass/gremio-jenkins-example.git', credentialsId: 'github-vass'
    }
}
    stage ('maven build') {
            tools {
                   maven "maven-3"
            }
            steps {
                nodejs(nodeJSInstallationName: 'njs-16') {
                    sh "mvn clean install"
                }
            }
        }
        
    stage ('build image'){
    steps {
        script {
            docker.build("${params.NAME}:${env.BUILD_ID}")
        }
    }
}

    }

}
