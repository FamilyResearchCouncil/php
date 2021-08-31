#!/usr/bin/env groovy
node('master') {
    checkout scm
    docker.withRegistry('', 'dockerhub'){
        stage('build'){
            parallel([
                8.0: {
                    def image = docker.build("familyresearchcouncil/oracle-php", './8.0')
                    if( env.BRANCH_NAME == 'master' ){
                        image.push('8.0')
                    }
                }
            ])
        }
    }
}
