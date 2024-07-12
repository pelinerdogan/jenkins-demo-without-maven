node {
    gitProjectURL = 'https://github.com/ozanbozkurtt/simple-spring-boot.git'
    containerName = 'simple-java'
    latestTag = 'latest'
    branchName = 'main'
    dockerProjectURL = 'https://github.com/pelinerdogan/dockerfiles-demo.git'
    dockerBranchName = 'main'
    dockerProjectName = 'Dockerfile'
    sonarProjectKey = 'simple-java'     
    sonarLoginToken = 'sqa_0b63a57af05fe4efc3b5f7fa9e7cf10c2a312afd'     
    sonarHostUrl = 'http://192.168.184.128:9000'
    stage('Get Dockerfile repository') {
        fileOperations([folderCreateOperation('mytmp')])
        dir('mytmp') {
            checkout([$class: 'GitSCM', branches: [[name: "${dockerBranchName}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[ url: "${dockerProjectURL}"]]])
        }
    stage('Clone repository') {
        checkout([$class: 'GitSCM', branches: [[name: "${branchName}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[ url: "${gitProjectURL}"]]])        
    }        
        sh("cp mytmp/${dockerProjectName} .")
        
        fileOperations([folderDeleteOperation('mytmp')])
    }
    stage('Build & register') {
         def dockerHome = tool 'docker'
         env.PATH = "${dockerHome}/bin:${env.PATH}"
            
        
            docker.withRegistry('http://192.168.184.128:5000') {
                def customImage = docker.build("${containerName}")
                customImage.push("${latestTag}")
            
        }
    }
}
