node{
stage ('cloning the project from git'){
git 'https://github.com/openconfig/public.git'
}
stage('Sonarqube Analysis'){
def scannerHome = tool 'sonarqube';
withSonarQubeEnv('sonarqube'){
sh "${scannerHome}/bin/sonar-scanner \
-D sonar.login=admin \
-D sonar.password=Admin \
-D sonar.projectKey=sonarqubetestproject \
-D sonar.exclsions=vendor/**,resources/**,**/*.java \
-D sonar.host.url=http://192.168.145.135:9000/"
}
}
}
