:ExploreDevops:


--------------------------------------------------------
Tomcat Prerequisites Installation
--------------------------------------------------------
sudo apt update
sudo apt install openjdk-17-jre -y


-----------------------------------
Tomcat Installation
-----------------------------------
wget https://archive.apache.org/dist/tomca...
tar -xzvf apache-tomcat-8.5.24.tar.gz
sudo chown -R username:username apache-tomcat-8.5.24
sudo cp tomcat-users.xml apache-tomcat-8.5.24/conf/tomcat-users.xml
sudo cp context.xml apache-tomcat-8.5.24/webapps/manager/META-INF/context.xml
sudo sed -i "s/8080/8082/g" apache-tomcat-8.5.24/conf/server.xml


--------------------------------------
Nexus Installation Steps
-------------------------------------- 

sudo apt-get update
sudo apt install openjdk-8-jre-headless
cd /opt
sudo wget https://download.sonatype.com/nexus/3...
sudo tar -zxvf latest-unix.tar.gz
sudo mv /opt/nexus-3.62.0-01 /opt/nexus
sudo adduser nexus
provide password and enter
sudo chmod 755 /etc/sudoers
sudo vi /etc/sudoers
make this entry in file
nexus ALL=(ALL) NOPASSWD:ALL
sudo chown -R nexus:nexus /opt/nexus
sudo chown -R nexus:nexus /opt/sonatype-work
sudo vi  /opt/nexus/bin/nexus.rc
uncomment entry and place "nexus" in double quote
sudo vi /etc/systemd/system/nexus.service
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target

sudo systemctl start nexus

