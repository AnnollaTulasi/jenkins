pipeline{
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 10,unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    parameters{
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    stages{
        stage("Build"){
            steps{
                sh 'echo This is build'
                //sh 'sleep 10'
            }
        }
        stage("Test"){
            steps{
                sh 'echo This is branch "GIT_BRANCH'
            }
        }
        stage("Deploy"){
            when{
                branch 'production'
            }
            steps{
                sh 'echo This is deploy'
                //error 'pipeline failed'
            }
        }
        stage('Print Params'){
            steps{
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"
                echo "Added webhooh and pushing to git"
            }
        }
        stage('Approval'){
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
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