# [Hello World - Spark Java Framework](https://knative.dev/docs/serving/samples/hello-world/helloworld-java-spark/)


**#( 05/20/21@ 7:27PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark@release-0.23✔**

   mvn clean install
   
    [INFO] Scanning for projects...
    [INFO]
    [INFO] -----------------------< com.example:helloworld >-----------------------
    [INFO] Building helloworld 0.0.1-SNAPSHOT
    [INFO] --------------------------------[ jar ]---------------------------------
    [INFO]
    [INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ helloworld ---
    [INFO] Deleting /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target
    [INFO]
    [INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ helloworld ---
    [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
    [INFO] skip non existing resourceDirectory /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/src/main/resources
    [INFO]
    [INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ helloworld ---
    [INFO] Changes detected - recompiling the module!
    [WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
    [INFO] Compiling 1 source file to /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target/classes
    [INFO]
    [INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ helloworld ---
    [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
    [INFO] skip non existing resourceDirectory /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/src/test/resources
    [INFO]
    [INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ helloworld ---
    [INFO] No sources to compile
    [INFO]
    [INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ helloworld ---
    [INFO] No tests to run.
    [INFO]
    [INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ helloworld ---
    [INFO] Building jar: /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target/helloworld-0.0.1-SNAPSHOT.jar
    [INFO]
    [INFO] --- maven-assembly-plugin:3.1.1:single (make-assembly) @ helloworld ---
    Downloading from central: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.pom
    Downloading from snapshots: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.pom
    Downloading from maven: https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.pom
    Downloaded from maven: https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.pom (4.8 kB at 9.8 kB/s)
    Downloading from central: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.jar
    Downloading from snapshots: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.jar
    Downloading from maven: https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.jar
    Downloaded from maven: https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/4.0.0/plexus-archiver-4.0.0.jar (192 kB at 1.3 MB/s)
    Downloading from central: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.pom
    Downloading from snapshots: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.pom
    Downloading from maven: https://repo1.maven.org/maven2/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.pom
    Downloaded from maven: https://repo1.maven.org/maven2/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.pom (10 kB at 112 kB/s)
    Downloading from central: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.pom
    Downloading from snapshots: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.pom
    Downloading from maven: https://repo1.maven.org/maven2/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.pom
    Downloaded from maven: https://repo1.maven.org/maven2/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.pom (1.3 kB at 18 kB/s)
    Downloading from central: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.jar
    Downloading from central: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.jar
    Downloading from snapshots: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.jar
    Downloading from snapshots: https://maven-repo-1.explorys.net:443/artifactory/plugins-release/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.jar
    Downloading from maven: https://repo1.maven.org/maven2/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.jar
    Downloading from maven: https://repo1.maven.org/maven2/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.jar
    Downloaded from maven: https://repo1.maven.org/maven2/org/apache/felix/maven-bundle-plugin/3.3.0/maven-bundle-plugin-3.3.0.jar (224 kB at 549 kB/s)
    Downloaded from maven: https://repo1.maven.org/maven2/biz/aQute/bnd/biz.aQute.bndlib/3.3.0/biz.aQute.bndlib-3.3.0.jar (2.5 MB at 2.1 MB/s)
    [INFO] Building jar: /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target/helloworld-0.0.1-SNAPSHOT-jar-with-dependencies.jar
    [INFO]
    [INFO] --- maven-install-plugin:2.4:install (default-install) @ helloworld ---
    [INFO] Installing /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target/helloworld-0.0.1-SNAPSHOT.jar to /Users/dbuddenbaum/.m2/repository/com/example/helloworld/0.0.1-SNAPSHOT/helloworld-0.0.1-SNAPSHOT.jar
    [INFO] Installing /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/pom.xml to /Users/dbuddenbaum/.m2/repository/com/example/helloworld/0.0.1-SNAPSHOT/helloworld-0.0.1-SNAPSHOT.pom
    [INFO] Installing /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target/helloworld-0.0.1-SNAPSHOT-jar-with-dependencies.jar to /Users/dbuddenbaum/.m2/repository/com/example/helloworld/0.0.1-SNAPSHOT/helloworld-0.0.1-SNAPSHOT-jar-with-dependencies.jar
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time:  6.536 s
    [INFO] Finished at: 2021-05-20T19:27:46-04:00
    [INFO] ------------------------------------------------------------------------
**#( 05/20/21@ 7:27PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark@release-0.23✔**

   ./mvnw package && java -jar target/helloworld-0.0.1-SNAPSHOT-jar-with-dependencies.jar
   
    [INFO] Scanning for projects...
    [INFO]
    [INFO] -----------------------< com.example:helloworld >-----------------------
    [INFO] Building helloworld 0.0.1-SNAPSHOT
    [INFO] --------------------------------[ jar ]---------------------------------
    [INFO]
    [INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ helloworld ---
    [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
    [INFO] skip non existing resourceDirectory /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/src/main/resources
    [INFO]
    [INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ helloworld ---
    [INFO] Nothing to compile - all classes are up to date
    [INFO]
    [INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ helloworld ---
    [WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
    [INFO] skip non existing resourceDirectory /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/src/test/resources
    [INFO]
    [INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ helloworld ---
    [INFO] No sources to compile
    [INFO]
    [INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ helloworld ---
    [INFO] No tests to run.
    [INFO]
    [INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ helloworld ---
    [INFO]
    [INFO] --- maven-assembly-plugin:3.1.1:single (make-assembly) @ helloworld ---
    [INFO] Building jar: /Users/dbuddenbaum/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark/target/helloworld-0.0.1-SNAPSHOT-jar-with-dependencies.jar
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 2.906 s
    [INFO] Finished at: 2021-05-20T19:28:14-04:00
    [INFO] ------------------------------------------------------------------------
    [Thread-0] INFO org.eclipse.jetty.util.log - Logging initialized @115ms to org.eclipse.jetty.util.log.Slf4jLog
    [Thread-0] INFO spark.embeddedserver.jetty.EmbeddedJettyServer - == Spark has ignited ...
    [Thread-0] INFO spark.embeddedserver.jetty.EmbeddedJettyServer - >> Listening on 0.0.0.0:8080
    [Thread-0] INFO org.eclipse.jetty.server.Server - jetty-9.4.z-SNAPSHOT, build timestamp: 2017-11-21T16:27:37-05:00, git hash: 82b8fb23f757335bb3329d540ce37a2a2615f0a8
    [Thread-0] INFO org.eclipse.jetty.server.session - DefaultSessionIdManager workerName=node0
    [Thread-0] INFO org.eclipse.jetty.server.session - No SessionScavenger set, using defaults
    [Thread-0] INFO org.eclipse.jetty.server.session - Scavenging every 600000ms
    [Thread-0] INFO org.eclipse.jetty.server.AbstractConnector - Started ServerConnector@5e516f1c{HTTP/1.1,[http/1.1]}{0.0.0.0:8080}
    [Thread-0] INFO org.eclipse.jetty.server.Server - Started @242ms
    [qtp1145410795-16] INFO spark.http.matching.MatcherFilter - The requested route [/favicon.ico] has not been mapped in Spark for Accept: [image/webp,*/*]

**#( 05/20/21@ 7:49PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark@release-0.23✔**

   docker build -t dbuddenbaum/helloworld-java .
   
    [+] Building 1.1s (13/13) FINISHED
     => [internal] load build definition from Dockerfile                                                                                          0.0s
     => => transferring dockerfile: 37B                                                                                                           0.0s
     => [internal] load .dockerignore                                                                                                             0.0s
     => => transferring context: 2B                                                                                                               0.0s
     => [internal] load metadata for docker.io/library/openjdk:8-jre-alpine                                                                       1.0s
     => [internal] load metadata for docker.io/library/maven:3.5-jdk-8-alpine                                                                     1.0s
     => [builder 1/5] FROM docker.io/library/maven:3.5-jdk-8-alpine@sha256:72922abc95d38e02f750b34800239dc0e2c298e74bfdd970018367f0d9281d5c       0.0s
     => [internal] load build context                                                                                                             0.0s
     => => transferring context: 334B                                                                                                             0.0s
     => [stage-1 1/2] FROM docker.io/library/openjdk:8-jre-alpine@sha256:f362b165b870ef129cbe730f29065ff37399c0aa8bcab3e44b51c302938c9193         0.0s
     => CACHED [builder 2/5] WORKDIR /app                                                                                                         0.0s
     => CACHED [builder 3/5] COPY pom.xml .                                                                                                       0.0s
     => CACHED [builder 4/5] COPY src ./src                                                                                                       0.0s
     => CACHED [builder 5/5] RUN mvn package -DskipTests                                                                                          0.0s
     => CACHED [stage-1 2/2] COPY --from=builder /app/target/helloworld-0.0.1-SNAPSHOT-jar-with-dependencies.jar helloworld.jar                   0.0s
     => exporting to image                                                                                                                        0.0s
     => => exporting layers                                                                                                                       0.0s
     => => writing image sha256:df1be73f76af08488f4849e6d6f3a93448b4e84289aec92254ea7861062c28bb                                                  0.0s
     => => naming to docker.io/dbuddenbaum/helloworld-java

**#( 05/20/21@ 7:55PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/knative-docs/docs/serving/samples/hello-world/helloworld-java-spark@release-0.23✔**

   docker push dbuddenbaum/helloworld-java

    Using default tag: latest
    The push refers to repository [docker.io/dbuddenbaum/helloworld-java]
    dea577628c8b: Pushed
    edd61588d126: Mounted from library/openjdk
    9b9b7f3d56a0: Mounted from library/openjdk
    f1b5933fe4b5: Mounted from library/openjdk
    latest: digest: sha256:4cb427eb23f7d0890a37840a81180d04709e26cf63d51a121616574c0bc04637 size: 1158
    
    
**#( 05/20/21@ 8:17PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative/helloworld@master✗✗✗**

   kubectl create -f helloworldsp-svc.yaml
   
    service.serving.knative.dev/helloworld-java created    
    
**#( 05/20/21@ 8:23PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative/helloworld@master✗✗✗**

   kubectl config set-context --current --namespace=default
   
    Context "kubernetes-admin@kubernetes" modified.    
    
**#( 05/20/21@ 8:24PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative/helloworld@master✗✗✗**

   kubectl get ksvc helloworld-java  --output=custom-columns=NAME:.metadata.name,URL:.status.url
   
    NAME              URL
    helloworld-java   http://helloworld-java.default.example.com    
    
**#( 05/20/21@ 8:44PM )( dbuddenbaum@dbuddenbaum-mbp ):~/Documents/rPi4/kalaxy/yaml/knative/helloworld@master✗✗✗**

   kubectl get svc $INGRESSGATEWAY --namespace istio-system
   
    NAME                    TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                                                                      AGE
    istio-ingressgateway    LoadBalancer   10.105.174.137   192.168.2.17   15021:31294/TCP,80:31844/TCP,443:30580/TCP,15012:31680/TCP,15443:31191/TCP   168m
    istiod                  ClusterIP      10.99.168.230    <none>         15010/TCP,15012/TCP,443/TCP,15014/TCP                                        169m
    knative-local-gateway   ClusterIP      10.110.187.116   <none>         80/TCP                                                                       130m    