pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk8'
    }
    parameters {
        booleanParam(name: "Perform release ?", description: '', defaultValue: false)
    }
    stages {
        stage('Initialize') {
            steps {
                bat '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Build') {
            steps {
                bat 'echo mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                bat 'echo mvn test'
            }
        }

        stage('Deploy') {
            steps {
                configFileProvider(
                    [configFile(fileId: 'f8069f73-6367-4fc5-a6d6-813eb424b54d', variable: 'MAVEN_GLOBAL_SETTINGS')]
                    ) {
                    bat 'echo mvn -gs %MAVEN_GLOBAL_SETTINGS deploy'
                    }
            }
            }
      /*   stage('Release') {
            when { expression {  params['Perform release ?']} }
            steps {
                script{
                    pom = readMavenPom file: 'pom.xml'
                }
                withCredentials([usernamePassword(credentialsId: 'ajaffrelot', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]){
                    //withMaven(mavenSettingsConfig: 'maven-config', globalMavenSettingsConfig: 'global-config') {
                        bat 'git config --global user.email "annaelleaffrelot@outlook.fr"'
                        bat 'git config --global user.name "ajaffrelot"'
                        bat 'git branch release/'+pom.version.replace("-SNAPbatOT","")
                        bat 'git push origin release/'+pom.version.replace("-SNAPSHOT","")
                        bat 'mvn release:prepare -s C:/Utilisateurs/annae/.m2/settings.xml -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                        bat 'mvn release:perform -s C:/Utilisateurs/annae/.m2/settings.xml -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                    //}
                }
            }
        }
        stage('Sonar') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'ajaffrelot', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]) {
                    bat "mvn  -s C:/Utilisateurs/annae/.m2/settings.xml sonar:sonar -Dsonar.login=admin -Dsonar.password=admin123"
                }
                }} */
