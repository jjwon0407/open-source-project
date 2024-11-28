pipeline {
    agent any
    environment {
        GITHUB_TOKEN = credentials('GitHub')  // 설정한 GitHub Token
    }
    stages {
        stage("Clone Repository") {
		steps {
        	        // git 명령어는 steps 블록 안에 위치
                	git url: 'https://github.com/jjwon0407/open-source-project.git', branch: 'main'
           	 }

        }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("jjwon0407/nogeut")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'jjwon0407') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
    }    
}
