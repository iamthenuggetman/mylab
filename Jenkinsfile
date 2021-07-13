pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/com.vinaysdevopslab-0.0.8.war', type: 'war']], credentialsId: '54b85066-304b-40b5-a8af-fc52c2c323ce', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.24:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'VinaysDevOpsLab-SNAPSHOT', version: '0.0.8'
        }

        // Stage4 : Testing
        stage ('Deploying'){
            steps {
                echo ' Deploying......'

            }
        }
        
    }

}