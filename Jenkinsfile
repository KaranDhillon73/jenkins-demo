pipeline {
    agent any
    stages  {
        stage('Git clone')    {
            steps {
                echo 'Git clone started'
                git 'https://github.com/KaranDhillon73/jenkins-demo.git'
                echo 'Git clone completed'
            }
        }
        stage('Maven build')    {
            steps {
                echo 'Maven Build Started'
                withMaven(globalMavenSettingsConfig: '', jdk: 'java11', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                    bat 'mvn -f MavenProject/ clean package'
                }
                echo 'Maven Build Completed'
            }
        }
        stage('Archive')    {
            steps {
                echo 'Archiev Started'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
                echo 'Archiev Completed'
            }
        }
        stage('deploy tomcat 8')    {
            steps {
                echo 'deployment to tomcat 8 started'
                deploy adapters: [tomcat8(credentialsId: '011dff00-5d7a-49d3-bd72-20a30ac57678', path: '', url: 'http://127.0.0.1:8082/')], contextPath: 'Module10Application', onFailure: false, war: '**/*.war'
                echo 'deployment to tomcat 8 completed'
            }
        }
        stage('Send mail')    {
            steps {
                echo 'Sending mail to recipients'
                emailext body: 'this is test email', subject: 'Module10_Build_details', to: 'karan.dhillon73@gmail.com'
                echo 'Sent mail to recipients'
            }
        }
  }
}
