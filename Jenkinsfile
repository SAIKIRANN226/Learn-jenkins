pipeline {
    agent {
        node {
            label 'saikiran-agent'  // Provide the same name what you have created in the jenkins
        }
    }
    environment {  // We have lot of environments we can select anything as per our requirement as of now we selected Greetings, if you want to know all environments just "env" and run it, it will show all available environments in the jenkins console
        GREETING = 'Hello Jenkins'
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()  // It will prevent from running parallel builds or It wont allow to run two builds at a time
    }
    parameters { // Parameters will not shown in the console when you build the job for the first time from the second time it will show then option called "Build with parameters"
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something') // Generally it is a dropdown we put options like dev,sit,uat,prod

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    // build
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                sh """
                    echo  "Here I wrote shell script" 
                    echo "$GREETING"
                    # sleep 10
                """
            }
        }
        stage('check params'){
            steps{
                sh """
                    echo "Hello ${params.PERSON}"

                    echo "Biography: ${params.BIOGRAPHY}"

                    echo "Toggle: ${params.TOGGLE}"

                    echo "Choice: ${params.CHOICE}"

                    echo "Password: ${params.PASSWORD}"
                """
            }
        }
    }
    // In Post build we have different conditions like always,changed,fixed,regression,oborted,failure,success,unstable,unsuccessful,cleanup, we use only few
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}
