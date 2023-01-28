


opis w Description w Jenkinsie:
http://localhost:8080/job/firstProject/

Projekt test-sample-maven-project
Nazwa projektu: firstProject
to już robisz po wszystkich instalacjach lokalnych: docker / nexus / jenkins
aplikacja do testowania: c:\Users\Jacek\Documents\GitHub\test-sample-maven-project\
git: https://github.com/j4sysiak/test-sample-maven-project

odpalasz Ubuntu 20.04 LTS  (z wsl2 windowsa)
odpalasz dockera z Ubuntu:  sudo dockerd
odpalasz Jenkinsa z Ubuntu: sudo service jenkins start  / http://localhost:8080  admin / admin  (czekaj z 5 min aż się to gówno uruchomi ...)

odpalasz nexusa z Ubuntu:   powinien się sam uruchomić ze startem dockera
docker ps
CONTAINER ID   IMAGE             COMMAND                  CREATED      STATUS         PORTS                                       NAMES
53af593a1c94   sonatype/nexus3   "/opt/sonatype/nexus…"   6 days ago   Up 6 minutes   0.0.0.0:8081->8081/tcp, :::8081->8081/tcp   jacek_nexus_1

http://localhost:8081/#browse/browse:test-sample-maven-project-release      admin / admin



-------------------- jak uruchomić builda w Jenkinsi, żeby pojawił się jar w Nexusie--------------------------
ważna jest wersja w konfiguracji:  0.0.9  - taka wersja objawi się w nexusie w repozytorium:
http://localhost:8081/#browse/browse:test-sample-maven-project-release

w InteliJ na projekcie starujesz w pliku pom.xml wersją np. 0.0.9 i robisz builda (mvn clean package) - powstaje plik jar:
C:\Users\Jacek\Documents\GitHub\test-sample-maven-project\target\offers-0.0.9.jar
robisz commit i push go gita.
i teraz zmieniasz wersję w Jenkinsie w konfiguracji (repozytorium nexusa) na 0.0.9 i nazwę pliku target\offers-0.0.9.jar

i uruchamiamy joba: Urchom

jak się build na Jenkinsie uda to powstanie w Nexusie wersja:

http://localhost:8081/#browse/browse:test-sample-maven-project-release:flipkart%2Foffers%2F0.0.9%2Foffers-0.0.9.jar