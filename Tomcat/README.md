# Apache Tomcat Installation with Systemd

This repository documents the steps to install and configure **Apache Tomcat 10** on a Linux server and run it as a **systemd service**.  
Using systemd allows Tomcat to be managed easily with `systemctl` commands and to start automatically on server boot.

---

## Prerequisites

- Linux server (Ubuntu / CentOS / Amazon Linux)
- Java Runtime Environment (JRE) installed
- Root or sudo privileges

---

## Step 1: Download Apache Tomcat

```bash
wget https://archive.apache.org/dist/tomcat/tomcat-10/v10.1.28/bin/apache-tomcat-10.1.28.tar.gz
```

---

## Step 2: Extract Tomcat

```bash
tar xzvf apache-tomcat-10.1.28.tar.gz
```

---

## Step 3: Create Tomcat User

Create a dedicated user to run Tomcat securely.

```bash
useradd --home-dir /opt/tomcat --shell /sbin/nologin tomcat
```

---

## Step 4: Copy Tomcat Files

Move the extracted files to the Tomcat directory.

```bash
cp -r apache-tomcat-10.1.28/* /opt/tomcat/
```

---

## Step 5: Set Ownership

Give the Tomcat user ownership of the directory.

```bash
chown -R tomcat.tomcat /opt/tomcat/
```

---

## Step 6: Create Systemd Service

Create a service file:

```bash
vim /etc/systemd/system/tomcat.service
```

Add the following configuration:

```
[Unit]
Description=Tomcat
After=network.target

[Service]
Type=forking
User=tomcat
Group=tomcat
WorkingDirectory=/opt/tomcat

Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINE_BASE=/opt/tomcat

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

[Install]
WantedBy=multi-user.target
```

---

## Step 7: Reload Systemd

```bash
systemctl daemon-reload
```

---

## Step 8: Start Tomcat

```bash
systemctl start tomcat
```

Check the service status:

```bash
systemctl status tomcat
```

---

## Step 9: Enable Tomcat on Boot

```bash
systemctl enable tomcat
```

---

## Useful Commands

Start Tomcat:

```bash
systemctl start tomcat
```

Stop Tomcat:

```bash
systemctl stop tomcat
```

Restart Tomcat:

```bash
systemctl restart tomcat
```

Check service status:

```bash
systemctl status tomcat
```

---

## Learning Outcomes

- Installing Apache Tomcat manually on Linux
- Creating a dedicated service user
- Managing services with **systemd**
- Using `systemctl` for service control
- Basic Linux server administration

---

## Author

Mashrur Hossain Khan
