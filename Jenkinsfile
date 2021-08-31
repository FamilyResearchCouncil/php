#!/usr/bin/env groovy
node('master') {
    checkout scm
    docker.withRegistry('', 'dockerhub-creds'){
        stage('build'){
            parallel([
                8.0: {
                    def image = docker.build("familyresearchcouncil/php:8.0-fpm", './8.0')
                    if( env.BRANCH_NAME == 'master' ){
                        image.push()
                    }
                }
            ])
        }
    }
}
