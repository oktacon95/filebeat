timestamps {

 node () {

  stage ('checkout repository') {
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GitHub_User', url: 'https://github.com/oktacon95/filebeat']]]) 
  }
  stage ('build docker image') {
   sh "docker build -t myfilebeat ." 
  }
  stage ('stop old docker image') {
   sh "docker stop filebeat" 
  }
  stage ('create new docker container') {
   sh 'docker run -d --rm --name filebeat --network elknet -v /etc/filebeat/config/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /var/log/testlogs:/var/log/testlogs -p 5066:5066 myfilebeat'
  }
 }
}
