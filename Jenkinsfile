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

        stage('Prepare Manifest') {
            steps {
                // Tworzy katalog dla pliku manifestu, jeśli nie istnieje
                bat 'if not exist build\\manifest mkdir build\\manifest'
                // Tworzy plik manifestu z wpisem Main-Class
                bat 'echo Main-Class: com.example.Main > build\\manifest\\MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
                // Pakowanie skompilowanych klas do pliku JAR
                bat 'if not exist build\\jar mkdir build\\jar'
                bat 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvmf ..\\..\\manifest\\MANIFEST.MF ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                bat '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
        
    }
}
