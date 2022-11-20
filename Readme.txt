------------------  on Ubuntu bez Dockera ------------------------------------------------------
nexus, jenkins bez Dockera 

to już robisz po wszystkich instalacjach lokalnych: docker / nexus / jenkins
aplikacja do testowania: /opt/sample-maven-project
git: https://github.com/gouthamchilakala/sample-maven-project
https://www.youtube.com/watch?v=yZFvJEygn_g
c:\Users\Jacek\Documents\JAVA\Moje_przydatne_polecenia\Jenkins Nexus Integration.txt

uruchamiasz Ubuntu 20.04 LTS  (z wsl2 windowsa)
uruchamiasz dockera z Ubuntu:  sudo dockerd
uruchamiasz Jenkinsa z Ubuntu: sudo service jenkins start  
sudo service jenkins status
odpalasz w przeglądrce http://localhost:8081/#browse/welcome   admin / admin




-----------------------------------------------------




-----------------------  installing Maven on Ubuntu  (bez Dockera):
najpierw instalujemy Maven 3.8.6.
c:\Users\Jacek\Documents\JAVA\Moje_przydatne_polecenia\Maven install on Ubuntu.txt

potem połaczenie Mavena z Jenkinsem:
jacek@BERLIN:/opt$ su - root
Password: root
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 5.10.102.1-microsoft-standard-WSL2 x86_64)
root@BERLIN:~# cd /opt
root@BERLIN:/opt# ls
apache-maven-3.8.6  containerd  maven  sample-maven-project
root@BERLIN:/opt# id
uid=0(root) gid=0(root) groups=0(root)

tworzymy plik settle.xml w /root/.m2

<?xml version="1.0" encoding="UTF-8"?>

<settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">

  <!-- servers
   | This is a list of authentication profiles, keyed by the server-id used within the system.
   | Authentication profiles can be used whenever maven must make a connection to a remote server.
   |-->
  <servers>
        <server>
      <id>nexus</id>
      <username>admin</username>
      <password>admin</password>
    </server>
  </servers>

  <mirrors>
    <mirror>
          <id>central</id>
          <name>central</name>
          <url>http://localhost:8081/repository/maven-public/</url>
          <mirrorOf>*</mirrorOf>
    </mirror>
        <!--
        <mirror>
          <id>maven-default-http-blocker</id>
      <mirrorOf>external:http:*</mirrorOf>
      <name>Pseudo repository to mirror external repositories initially using HTTP.</name>
      <url>http://0.0.0.0/</url>
      <blocked>true</blocked>
    </mirror>-->
  </mirrors>

</settings>



to dodajemy do pom.xml:

    <!-- NEXUS ustawienia settle.xml z pliku settle.xml w lokalizacji /root/.m2 -->
    <distributionManagement>
        <repository>
            <id>nexus</id>
            <name>maven-releases</name>
            <url>http://localhost:8081/repository/maven-releases/</url>
        </repository>
        <snapshotRepository>
            <id>nexus</id>
            <name>maven-snapshots</name>
            <url>http://localhost:8081/repository/maven-snapshots/</url>
        </snapshotRepository>
    </distributionManagement>


root@BERLIN:/opt/sample-maven-project# pwd
/opt/sample-maven-project
root@BERLIN:/opt/sample-maven-project# ls
pom.xml  src  target

odpalamy:
mvn clean compile
mvn package
mvn deploy

w zależności, czy w pom mamy release, czy SNAPSHOT (musi być z dużych liter):
to odłoży nam się wersja w nexus:

dla: <version>1.2-release</version>
http://localhost:8081/#browse/browse:maven-releases



dla:
<version>1.3-SNAPSHOT</version>
http://localhost:8081/#browse/browse:maven-snapshots



