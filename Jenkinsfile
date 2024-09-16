node('dev') 
{
    stage('Get repository'){
        git branch: 'main', url: 'https://github.com/ApasoftTraining/jenkins-scripted1.git'
    }

    stage('Compile') {
        echo 'Compiling the Java Maven project...'        
        // We run the Maven command to compile
        sh 'mvn clean compile'
    }

    stage('Test') {
        echo 'Running tests on the Java Maven project...'
        // We run the project's unit tests
        sh 'mvn test'
    }

    stage('Execute Program') {
        echo 'Executing the Java program that processes VISA card numbers...'
        // We run the Java program that divides the VISA card numbers
        sh 'mvn exec:java -Dexec.mainClass="com.example.CardProcessor" -Dexec.args="4111111111111111"'
        //We save the generated target to use it in a later node
        stash includes: 'target*/**', name: 't1'
    }
}

node('prod') {
    stage('Deploy') {
        //We unpack the target on the new node
        unstash 't1'
        echo 'Deploying the application to production...'
        // We copy the artifact to the /home/jenkins/app directory on the production node
        sh 'mkdir /home/jenkins/jenkins-app/'
        sh 'cp -r target/* /home/jenkins/jenkins-app/'
        echo 'Deployment completed!'
    }
}
