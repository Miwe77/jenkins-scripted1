node('dev') 
{
    stage('Compile') {
        echo 'Compiling the Java Maven project...'
        // Clonamos el código fuente desde el repositorio
        git 'https://your-repo-url.git'
        
        // Ejecutamos el comando Maven para compilar
        sh 'mvn clean compile'
    }

    stage('Test') {
        echo 'Running tests on the Java Maven project...'
        // Ejecutamos las pruebas unitarias del proyecto
        sh 'mvn test'
    }

    stage('Execute Program') {
        echo 'Executing the Java program that processes VISA card numbers...'
        // Ejecutamos el programa Java que divide los números de la tarjeta VISA
        sh 'mvn exec:java -Dexec.mainClass="com.example.CardProcessor" -Dexec.args="4111111111111111"'
    }
}

node('prod') {
    stage('Deploy') {
        echo 'Deploying the application to production...'
        // Copiamos el artefacto al directorio /home/jenkins/app en el nodo de producción
        sh 'cp -r target/* /home/jenkins/app/'
        echo 'Deployment completed!'
    }
}
