#!/usr/bin/env groovy
node('master') {
    checkout scm
    docker.withRegistry('', 'dockerhub-creds'){
        stage('build'){
            parallel([
                (7.4): {
                    def image = docker.build("familyresearchcouncil/php:7.4-fpm", './7.4')
                    if( env.BRANCH_NAME == 'master' ){
                        image.push()
                    }
                },
                (7.4-dev): {
                    def image = docker.build("familyresearchcouncil/php:7.4-fpm-dev", './7.4-dev')
                    if( env.BRANCH_NAME == 'master' ){
                        image.push()
                    }
                },
                (8.0): {
                    def image = docker.build("familyresearchcouncil/php:8.0-fpm", './8.0')
                    if( env.BRANCH_NAME == 'master' ){
                        image.push()
                    }
                },
                (8.0-dev): {
                    def image = docker.build("familyresearchcouncil/php:8.0-fpm-dev", './8.0-dev')
                    if( env.BRANCH_NAME == 'master' ){
                        image.push()
                    }
                }
            ])
        }
    }
}
