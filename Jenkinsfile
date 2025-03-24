pipeline{
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 10,unit: 'SECONDS')
    }
    stages{
        stage("Build"){
            steps{
                sh 'echo This is build'
                sh 'sleep 10'
            }
        }
        stage("Test"){
            steps{
                sh 'echo This is test'
            }
        }
        stage("Deploy"){
            steps{
                sh 'echo This is deploy'
                //error 'pipeline failed'
            }
        }
    }
    post{
        always{
            sh 'echo this section always runs'
            deleteDir()
        }
        success{
            echo "This section runs when the build is success"
        }
        failure{
            echo "This section run during failure of the job"
        }
    }
}