pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh './mvnw clean package -Dmaven.test.skip=true '
//         sh 'docker --version'
//         sh 'docker build -f . --tag pet .'
      }
    }

    stage('sonar') {
      steps {
        sh "./mvnw sonar:sonar -Dsonar.host.url=http://sonarqube-container:9000 -Dsonar.login=admin -Dsonar.password=admin"
      }
    }

    stage('run') {
      steps {
        sh '''
        ansible --version
        '''
        sh 'cp -r target/ /shared/target'
        sh 'ansible-playbook playbooks/playbook.yml'
//         sh 'JENKINS_NODE_COOKIE=dontKillMe nohup java -jar /shared/target/*.jar &'
        

      }
    }

  }
}
