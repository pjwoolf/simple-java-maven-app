node {
    stage('Build') {
        checkout scm
        docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
            sh 'mvn -B -DskipTests clean package'
        }
    }   
    stage('Test') { 
        try {
            checkout scm
            docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
                sh 'mvn test'
            } 
        } catch (e) {
            throw e
        } finally {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
