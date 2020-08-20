node{
    stage("Git Clone"){
        git url: "https://github.com/jc-ec-org/spring-boot-mongo-docker.git",branch: "master"
    }
    stage("Build Package"){
        def maven_H=tool name: "Maven", type: "maven"
        sh "${maven_H}/bin/mvn clean package"
    }
    stage("Build Docker Image"){
        sh "docker build -t jcheeran/spring-boot-mongodb-docker:${buildNum} ."
    }
    stage("Docker Login and Push")
    {
        withCredentials([string(credentialsId: 'DockerHubPwd', variable: 'DockerHubPwd')]) 
        {
         sh "docker login -u jcheeran -p ${DockerHubPwd}"
        }
       sh "docker push jcheeran/spring-boot-mongodb-docker:${buildNum}"
    }
    
}
