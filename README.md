# Tomcat-installation

sudo apt-get update
sudo apt-get install default-jdk
sudo mkdir /opt/tomcat
sudo tar xzvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1
cd /opt/tomcat
sudo chgrp -R tomcat /opt/tomcat
sudo chown -R tomcat webapps/ work/ temp/ logs/




Step 5: Create a systemd Service File
sudo update-java-alternatives -l
/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
sudo nano /etc/systemd/system/tomcat.service
  /etc/systemd/system/tomcat.service
  -------------------------------------------------------------------------------------------------------------------------------
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
-------------------------------------------------------------------------------------------------------------------------------------

sudo systemctl daemon-reload
