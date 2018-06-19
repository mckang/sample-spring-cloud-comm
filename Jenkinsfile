node('dind-node-1') {
        withMaven(maven:'M3') {
          stage('Checkout') {
           git url: 'https://github.com/mckang/sample-spring-cloud-comm.git',
credentialsId: 'bbddd56d-2a6c-4972-b160-89791998568c',
branch: 'master'                   
  }
  stage('Build') {
   dir('account-service') {
    sh 'mvn clean install'
   }
branch: 'master'
   def pom = readMavenPom file:'pom.xml'
   print pom.version
   env.version = pom.version
   currentBuild.description = "Release: ${env.version}"
}
  stage('Image') {
   dir ('account-service') {
    def app = docker.build "mckang/account-service:${env.version}"
app.push() }
}
  stage ('Run') {
   docker.image("mckang/account-service:${env.version}").run('-p
8091:8091 -d --name account --network sample-spring-cloud-network')
  }
} }
