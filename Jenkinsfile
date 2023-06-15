node {
    checkout scm
    docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }   
        stage('Test') { 
            try {
                sh 'mvn test'
            } catch (e) {
                throw e
            } finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
        }
    }
}
