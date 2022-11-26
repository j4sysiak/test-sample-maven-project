https://www.youtube.com/watch?v=yZFvJEygn_g

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

    <distributionManagement>
        <repository>
            <id>nexus-from-m2</id>
            <name>maven-release</name>
            <url>http://localhost:9081/nexus/content/repositories/maven-release</url>
        </repository>
        <snapshotRepository>
            <id>nexus-from-m2</id>
            <name>maven-snapshots</name>
            <url>http://localhost:9081/nexus/content/repositories/maven-snapshots</url>
        </snapshotRepository>
    </distributionManagement>


    ----------------------------------

    nvn clean package
    mnv deploy
    lub:
    mvn clean deploy -P release


    w pomie sterujemy wersjami:
    <!--  <version>1.5-SNAPSHOT</version>-->
        <version>1.6-RELEASE</version>

        w zależności co wybierzemy RELEASE/SNAPSHOT taka wesja binarek *.JAR pojawi się na Nexus w odpowiednich lokalizacjach:
        - http://localhost:9081/nexus/content/repositories/maven-release   dla <version>1.6-RELEASE</version>
        - http://localhost:9081/nexus/content/repositories/maven-snapshots   dla <version>1.6-SNAPSHOT</version>

