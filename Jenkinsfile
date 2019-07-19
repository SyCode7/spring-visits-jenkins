node {

    withMaven(maven:'maven') {

        stage('Checkout') {
            git url: 'https://github.com/SyCode7/spring-visits-jenkins.git', credentialsId: 'SyCode7-@secure&sons7', branch: 'master'
        }

        stage('Build') {
            sh 'mvn clean install -DskipTests'

            def pom = readMavenPom file:'pom.xml'
            print pom.version
            env.version = pom.version
        }

        stage('Image') {
            dir ('spring-visits-jenkins') {
                def app = docker.build "localhost:5000/spring-visits-jenkins:${env.version}"
                app.push()
            }
        }

  
        
    }

}
