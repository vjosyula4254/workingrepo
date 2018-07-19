#!groovy

pipeline {
    agent any
    tools {
        maven 'Maven'
        nodejs 'NodeJS'
    }
    stages {
            stage('Clean') {
                steps {
                dir('edge') {
                    bat "mvn clean"
                }
            }
        }

            stage('Pre-Deployment Configuration - Caches') {
                steps {
                    dir('edge') {
                    println "Predeployment of Caches "
                    bat "mvn apigee-config:caches " +
                            "    -Papigee -Denv=${params.apigee_env} -Dorg=${params.apigee_org} " +
                            "    -Dusername=${params.apigee_user} " +
                            "    -Dpassword=${params.apigee_pwd}"

                }
            }
        }

            stage('Pre-Deployment Configuration - targetservers') {
                steps {
                    dir('edge') {
                    println "Predeployment of targetservers "
                    bat "mvn apigee-config:targetservers " +
                            "    -Papigee -Denv=${params.apigee_env} -Dorg=${params.apigee_org} " +
                            "    -Dusername=${params.apigee_user} " +
                            "    -Dpassword=${params.apigee_pwd}"

                }
            }
        }

            stage('Pre-Deployment Configuration - keyvaluemaps ') {
                steps {
                    dir('edge') {
                    println "Predeployment of keyvaluemaps  "
                    bat "mvn apigee-config:keyvaluemaps " +
                            "    -Papigee -Denv=${params.apigee_env} -Dorg=${params.apigee_org} " +
                            "    -Dusername=${params.apigee_user} " +
                            "    -Dpassword=${params.apigee_pwd}"

                }
            }
        }

            stage('Build proxy bundle') {
                steps {
                    dir('edge') {
                    bat "mvn package -Papigee -Denv=${params.apigee_env} -Dorg=${params.apigee_org}"

                }
            }
        }

            stage('Deploy proxy bundle') {
                steps {
                    dir('edge') {
                    bat "mvn apigee-enterprise:deploy -Papigee -Denv=${params.apigee_env} -Dorg=${params.apigee_org} -Dusername=${params.apigee_user} -Dpassword=${params.apigee_pwd}"
                }
            }
        }
        
    }
}
