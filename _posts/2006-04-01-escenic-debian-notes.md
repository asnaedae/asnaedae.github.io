---
layout: post
tags:
  - escenic
  - tomcat
  - java
redirect_from:
  - /2006/04/01/escenic-debian-notes/
  - /escenic-debian-notes/
title:
---

### NON-FREE APT REPOSITORIES
Install openssh package if not already installed

```bash
# apt-get install openssh-server
```
Add the following to /etc/apt/sources.list:

```bash
deb http://oss.oracle.com/debian unstable main non-free
deb http://ftp.uk.debian.org/debian etch main contrib non-free
# apt-get update
```
Install Async IO library for Oracle

```bash
# apt-get install libaio
```
Install optional extras for converting the JVM to a .deb

```bash
# apt-get install build-essential fakeroot java-package
# download sun binary JDK
```
Create the ”deb” package:

```bash
$ su - escenic
# fakeroot make-jpkg jdk-1_5_0_14-linux-i586.bin
# exit
$ dpkg -i sun-j2sdk1.5_1.5.0+update14_i386.deb
```
Check that the above JVM is in use

```bash
# update-alternatives --config java
```
Install ant

```bash
# apt-get install ant-optional
```
Install openldap

```bash
# apt-get install slapd
```
Convert/start/install base-ldif according to the ECE install guide
Now – after oracle-xe is installed you’ll need to configure it to allow all net access, else you’ll be stuck doing:-

```bash
$ ssh -l USERNAME HOSTNAME -L 8080:localhost:8080
```
This can be done by:

```bash
# su - oracle
$ sqlplus -S system/password@//localhost/XE < EXEC DBMS_XDB.SETLISTENERLOCALACCESS(FALSE);
EXIT;
/
!
```
Escenic bits

```bash
# scp *escenic*jar root@HOSTNAME:/opt/escenic/src/
# cd /opt/escenic
# jar xvf src/engine*jar
# ln -s engine-4.3-2/ engine
```
Configure the build environment

```bash
# mkdir build && cd build && jar xvf ../src/assemb*jar
# ant -q initialize
```
Check location for engine.root

```bash
# vi assemble.properties
# ant -q ear
```
Check Oracle environment

```bash
ORACLE_HOME=/usr/lib/oracle/xe/app/oracle/product/10.2.0/server
PATH=$PATH:$ORACLE_HOME/bin
if [ -e $ORACLE_HOME/bin/oracle_env.sh ]; then
  source $ORACLE_HOME/bin/oracle_env.sh
elif [ -e $ORACLE_HOME/..//client/bin/oracle_env.sh ]; then
  source $ORACLE_HOME/../client/bin/oracle_env.sh
fi
export PATH ORACLE_HOME
```
Add the following to /etc/default/tomcat5.5

```bash
# Escenic Customisations
#
ESCENIC_ROOT=/opt/web/escenic/engine
ESCENIC_LOCALCONFIG=/opt/web/escenic/engine/localconfig
IP=`/usr/local/bin/ece_ip`
echo "Using IP $IP for local host address"
ESCENIC_OPTS=" -Descenic.root=$ESCENIC_ROOT"
ESCENIC_OPTS="$ESCENIC_OPTS -Dneo.nursery.GlobalBus.root=$ESCENIC_LOCALCONFIG/"
ESCENIC_OPTS="$ESCENIC_OPTS -Djava.security.auth.login.config=$ESCENIC_ROOT/security/jaas.config"
ESCENIC_OPTS="$ESCENIC_OPTS -Djava.security.policy=$ESCENIC_ROOT/security/java.policy"
ESCENIC_OPTS="$ESCENIC_OPTS -Dneo.util.cache.IOSocketFactory.next=com.css.rmi.ServerTwoWaySocketFactory"
ESCENIC_OPTS="$ESCENIC_OPTS -Djava.rmi.server.hostname=`/usr/local/bin/ece_ip`"
ESCENIC_OPTS="$ESCENIC_OPTS -Dorg.xml.sax.driver=org.apache.xerces.parsers.SAXParser"
ESCENIC_OPTS="$ESCENIC_OPTS -Djavax.xml.parsers.SAXParserFactory=org.apache.xerces.jaxp.SAXParserFactoryImpl"
ESCENIC_OPTS="$ESCENIC_OPTS -Djavax.xml.parsers.DocumentBuilderFactory=org.apache.xerces.jaxp.DocumentBuilderFactoryImpl"
ESCENIC_OPTS="$ESCENIC_OPTS -Djavax.xml.transform.TransformerFactory=org.apache.xalan.processor.TransformerFactoryImpl"
ESCENIC_OPTS="$ESCENIC_OPTS -Djava.awt.headless=true"
export ESCENIC_OPTS
CATALINA_OPTS="-server $ESCENIC_OPTS"
```
### ECE_IP

```bash
$ more ece_ip
#!/bin/sh
IF_LIST="eth1 eth0 eth1"
for IF in $IF_LIST
do
IP=`ifconfig $IF 2>/dev/null | \
		grep "inet addr" | \
		tr ':' ' ' | \
        awk '{print $3}'`
if [ "X$IP" != "X" ]; then
echo $IP
break
fi
IP=127.0.0.1
done
```
### ECE_Update_localconfig

```bash
#!/bin/sh
ECE_BASE=/opt/web/escenic/engine/localconfig
if [ "X$1" != "X" ]; then
	ECE_BASE=$1
fi
IP=`/usr/local/bin/ece_ip`
echo "IP: $IP"
perl -pi -e "s,rmiServer=rmi://.*:8123,rmiServer=rmi://$IP:8123," \
$ECE_BASE/com/escenic/studio/StudioConfig.properties
perl -pi -e "s,host=.*,host=$IP," \
$ECE_BASE/RMI.properties
perl -pi -e "s,webPublicationRoot=http://.*:,webPublicationRoot=http://$IP:," $ECE_BASE/ServerConfig.properties
```

```bash
sveds:/etc/init.d# update-rc.d escenic-sveds defaults 89
Adding system startup for /etc/init.d/escenic-sveds ...
/etc/rc0.d/K89escenic-sveds -> ../init.d/escenic-sveds
/etc/rc1.d/K89escenic-sveds -> ../init.d/escenic-sveds
/etc/rc6.d/K89escenic-sveds -> ../init.d/escenic-sveds
/etc/rc2.d/S89escenic-sveds -> ../init.d/escenic-sveds
/etc/rc3.d/S89escenic-sveds -> ../init.d/escenic-sveds
/etc/rc4.d/S89escenic-sveds -> ../init.d/escenic-sveds
/etc/rc5.d/S89escenic-sveds -> ../init.d/escenic-sveds
```
