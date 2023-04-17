## This is for Hadoop 3.3.5 if you are on a different version look for official documentation

![](assets/Satania_smug.jpg?raw=true)

### This guide assumes you have installed Hadoop

**Installing ssh (For Debian and Ubuntu based distros):**

```
sudo apt install ssh 
sudo apt install pdsh
```

**For Fedora: (Tested)**

```
sudo dnf install openssh
```

## Add Path to JAVA_HOME

```
export JAVA_HOME=/usr/lib/java-8-openjdk
```

## After the setup, try running 

```
hadoop version
```

## OR (If you didn't add the executable path to your shell)

```
bin/hadoop
```

### By default, Hadoop is configured to run in a non-distributed mode, as a single Java process. This is useful for debugging.

**The following example copies the unpacked conf directory to use as input and then finds and displays every match of the given regular expression. Output is written to the given output directory.**

```
mkdir input
cp etc/hadoop/*.xml input
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.5.jar grep input output 'dfs[a-z.]+'
cat output/*
```

## Configuration

**First Navigate to etc/hadoop directory inside Hadoop**

```
cd hadoop3.3.5/etc/hadoop
```

**Open it and Paste this core-site.xml (below <!-- Put site-specific property overrides in this file. --> )**


```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>

```

**And**

**This in hdfs-site.xml (below <!-- Put site-specific property overrides in this file. --> )**

```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

## Setup for password less ssh

### What is ssh ?
### Method to log in to computer from your PC using the Interwebs(Internet)
**For more info visit [here](https://www.howtogeek.com/311287/how-to-connect-to-an-ssh-server-from-windows-macos-or-linux/)**

**Now to check that you can ssh in to your localhost(Your own Pc) without a passphrase:**

```
ssh localhost
```

**if cannot, do this( For more about RSA key authentication for ssh, click [here](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server) )**


```
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```
