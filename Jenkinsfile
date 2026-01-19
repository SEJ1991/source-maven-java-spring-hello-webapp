pipeline {
  agent any

  triggers {
    pollSCM('* * * * *')   // ⏱ 매분 Git 변경 확인
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/SEJ1991/source-maven-java-spring-hello-webapp.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean package'
      }
    }

    stage('Deploy') {
      steps {
        deploy adapters: [
          tomcat9(
            credentialsId: '7c22256e-c2d6-4145-b5d5-00ba3b8833ac',
            url: 'http://192.168.76.102:8080'
          )
        ],
        contextPath: '',
        war: 'target/hello-world.war'
      }
    }
  }
}
