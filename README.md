*** DEVELOPING ***

== JAVA DEV ENV ==

# Build Java dev env image
sudo docker build -t amee/java-devenv:latest java/

# Run Java dev env image
sudo docker run --name javadevenv -d -v /usr/local/src/saimoon/AMEE-devenv/java/share:/opt/amee/dev amee/java-devenv

# Enter env
sudo docker exec -ti javadevenv bash



### Compile FLUME

rm -rf ~/.m2/repository/
git clone https://github.com/apache/flume.git
cd flume
git checkout flume-1.8
mvn clean install -DskipTests
cd flume-ng-sinks/flume-ng-morphline-solr-sink

mkdir /tmp/flume
cp -a target/dependency/ /tmp/flume/
cd ../../
cp -a flume-ng-dist/target/apache-flume-1.8.0-bin.tar.gz /tmp/flume/
cd /tmp/flume
tar xvf apache-flume-1.8.0-bin.tar.gz
cp dependency/*.jar apache-flume-1.8.0-bin/lib/
rm apache-flume-1.8.0-bin/lib/javax.servlet-3.0.0.v201112011016.jar 
rm apache-flume-1.8.0-bin/lib/xml-apis-1.3.04.jar

rm -rf rm apache-flume-1.8.0-bin.tar.gz dependency/
tar cvf apache-flume-1.8.0-bin-morphline.tar apache-flume-1.8.0-bin
gzip apache-flume-1.8.0-bin-morphline.tar

## Configure FLUME

# Edit vim bin/flume-ng, modify the following line:
JAVA_OPTS="-Xms100m -Xmx2000m"


