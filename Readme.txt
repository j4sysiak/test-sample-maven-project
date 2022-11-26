https://www.youtube.com/watch?v=yZFvJEygn_g

UWAGA!
ten kod musi być umieszczony na Ubuntu w lokalizacji /opt
robi to sie tak:
ten kod przenosimy na Git
a potem po zalogowaniu do Ubuntu przechodzimy do /opt i najpierw pobieramy kod
a potem standardowo : git add commit push pull itp.

    ----------------------------------
    UWAGA:  żeby otrzymać wersje w mexusie w repo snapshot i release to odpal te polecenia w mvn:
    mvn clean package
    mvn deploy
    lub:
    mvn clean deploy -P release


    w pomie sterujemy wersjami:
    <!--  <version>1.5-SNAPSHOT</version>-->
        <version>1.6-RELEASE</version>

        w zależności co wybierzemy RELEASE/SNAPSHOT taka wesja binarek *.JAR pojawi się na Nexus w odpowiednich lokalizacjach:
        - http://localhost:9081/nexus/content/repositories/maven-release   dla <version>1.6-RELEASE</version>
        - http://localhost:9081/nexus/content/repositories/maven-snapshots   dla <version>1.6-SNAPSHOT</version>



----------------------------------------------------
<!-- NEXUS ustawienia settle.xml z pliku lokalizacji: /root/.m2 /settle.xml-->

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
  </mirrors>




pom.xml

    <!-- NEXUS ustawienia settle.xml z pliku lokalizacji: /root/.m2 -->
    <distributionManagement>
        <repository>
            <id>nexus</id>
            <name>maven-release</name>
            <url>http://localhost:8081/repository/maven-releases/</url>
        </repository>
        <snapshotRepository>
            <id>nexus</id>
            <name>maven-snapshots</name>
            <url>http://localhost:8081/repository/maven-snapshots/</url>
        </snapshotRepository>
    </distributionManagement>


