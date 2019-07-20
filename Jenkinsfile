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
        
        stage('Make Container') {
            steps {
               sh 'docker build -f src/main/docker/Dockerfile -t ktorkura/visits-service-jenkins:${env.BUILD_ID}'
                   }
         }

        stage('Run') {
             sh 'mvn spring-boot:run'
        }

  
        
    }
    

}
