node {

    withMaven(maven:'maven') {

        stage('Checkout') {
            git url: 'https://github.com/SyCode7/spring-petclinic-microservices-swagger.git', credentialsId: 'SyCode7-@secure&sons7', branch: 'master'
        }

        stage('Build') {
            sh 'mvn clean install -DskipTests'

            def pom = readMavenPom file:'pom.xml'
            print pom.version
            env.version = pom.version
        }

        stage('Image') {
            dir ('spring-petclinic-customers-service') {
                def app = docker.build "localhost:5000/spring-petclinic-customers-service:${env.version}"
                app.push()
            }
        }

        stage ('Run') {
            docker.image("localhost:5000/spring-petclinic-customers-service:${env.version}").run('-p 1001:1001 -h customers --name customers --link discovery')
        }

        
    }

}
