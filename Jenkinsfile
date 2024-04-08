pipeline {
    agent any
    tools {
        // Użyj wersji JDK o nazwie "Java 21" skonfigurowanej w Jenkins
        jdk 'Java 21'
    }

    environment {
        // Definiowanie JAVA_HOME może być opcjonalne, zależnie od konfiguracji Jenkinsa
        JAVA_HOME = tool 'Java 21'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/por314ug/app-1.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                // Tworzenie katalogu dla skompilowanych klas
                bat 'if not exist build\\classes mkdir build\\classes'
                // Kompilacja Main.java
                bat '"%JAVA_HOME%\\bin\\javac" -d build\\classes Main.java'
            }
        }

        stage('Package') {
            steps {
                // Pakowanie skompilowanych klas do pliku JAR
                bat 'if not exist build\\jar mkdir build\\jar'
                bat 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvf ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                bat '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
        
    }
}
