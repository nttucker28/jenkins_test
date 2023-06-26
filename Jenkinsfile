pipeline {
    agent any
    tools { maven 'Maven LOCAL' }
    stages {
        stage ('Build') {
            steps {
                echo "build on main branch"
                //sh 'mvn clean package -DskiptTests=true'
                sh 'mvn clean install'
            }
        }
        stage ('Test') {
            parallel {
                stage('Test A') {
                    agent any
                    steps {
                        echo "This is test A on main branch"
                        sh "mvn test"
                    }
                }
                stage('Test B') {
                    agent any
                    steps {
                        echo "This is test B on main branch"
                        sh "mvn test"
                    }
                
                }
            }
            post {
                success {
                    echo "success on main branch"
                    /*dir("webapp/target/") {
                        stash name: "maven-build", includes: "*.war"
                    }*/
                }
            }
            
        }
        stage ('DeployDev') {
            when {branch 'Dev'
                beforeAgent true}
            agent any
            steps {
                echo "dev deploy on main branch"
                /*dir("/var/www/html") {
                    unstash "maven-build"
                }
                sh """
                cd /var/www/html/
                jar -xvf webapp.war
                """*/
            }
        }
        stage ('DeployProd') {
            when{branch 'master'
                beforeAgent true}
            agent any
            steps {
                echo "prod deploy on main branch"
                /*timeout(time:5, unit:'DAYS') {
                    input message: 'Deployment approved?'
                }
                dir("/var/www/html") {
                    unstash "maven-build"
                }
                sh """
                cd /var/www/html/
                jar -xvf webapp.war
                """*/
            }
        }
    }
}
