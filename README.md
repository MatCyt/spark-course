# Spark Course

This repository contains all necessary inputs to run the course hands-on labs. 

## Repository contents

* **Notebooks** : contains corresponding Jupyter Notenbooks for each lab
* **data** : contains input datasets for the labs
* **provision** : holds the bash provisioning scripts for the Virtual Machine
* **scripts** : useful scripts

## Software Setup

In order to boot-up the course virtual machine follow these steps:

1. Install VirtualBox manager : [link](https://www.virtualbox.org/)
2. Install Vagrant : [link](https://www.vagrantup.com/downloads.html)
3. Install Git : [link](https://git-scm.com/downloads)
4. Checkout the git repository to your computer:  
```
git clone https://github.com/bla/spark-course
```
5. Boot up the provide course image with Vagrant and wait for the VM to start-up. Then connect via ssh : 
```
cd spark-course 
vagrant up # *now wait, note this may take up to 15-20 min depending on machine*
vagrant ssh
```
6. Test Installation

Start up the pyspark shell
```
$SPARK_HOME/bin/pyspark
```

You should see a PySpark shell appearing looking like this:

<img src="images/pyspark-shell.png" width="700" height="400" align="centre">

Start up a Scala spark shell
```
$SPARK_HOME/bin/spark-shell
```

You should see a Scala shell appearing looking like this:

<img src="images/scala-shell.png" width="700" height="400" align="centre">

*Note:* subsequent vm start-ups only require : vagrant ssh from the spark-course directory 

## Hands-On Labs

These labs will be executed using the [Virtual Machine](https://en.wikipedia.org/wiki/Virtual_machine) created in the Software Setup. The VM runs a Linux Ubuntu 16.0.4 OS and has pre-installed the following software packages:

1. Java Open JDK 1.8
2. Apache Spark 2.2.0 (including Hadoop 2.6)
3. Anaconda Python 3.6
4. Apache Zepellin 0.7.3

In order to launch pyspark using jupyter notebook simple type:

```
start_notebook.sh
```

## Software Installation (from scratch)

Should you prefer to install all the software your own (beware it may take some time) follow these instructions:

First follow steps [1-5] specified in the Software Setup section above

Then, once you have logged in to the new VM:

0. Update ubuntu libs
```
apt-get update
mkdir  /usr/local/software/apache
```

1. Install Java 
```
sudo apt-get install openjdk-8-jre-headless -qq && apt-get clean
```
2. Install Firefox
```
sudo apt-get install firefox -qq && apt-get clean
```
3. Install Anaconda
```
curl -O -# https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
bash Anaconda3-5.0.1-Linux-x86_64.sh -b -p /usr/local/software/conda
```
4. Install Spark
```
curl -O -# http://mirror.cogentco.com/pub/apache/spark/spark-2.2.0/spark-2.2.0-bin-hadoop2.7.tgz
mv spark-2.2.0-bin-hadoop2.7.tgz /usr/local/software/apache
cd /usr/local/software/apache
tar zxf spark-2.2.0-bin-hadoop2.7.tgz
ln -s spark-2.2.0-bin-hadoop2.7.tgz spark
rm spark-2.2.0-bin-hadoop2.7.tgz
cd 	
```
5. Install Zepellin
```
curl -O -# http://mirrors.advancedhosters.com/apache/zeppelin/zeppelin-0.7.3/zeppelin-0.7.3-bin-all.tgz
mv zeppelin-0.7.3-bin-all /usr/local/software/apache
cd /usr/local/software/apache
tar zxf zeppelin-0.7.3-bin-all.tgz
ln -s zeppelin-0.7.3-bin-all zeppelin
rm zeppelin-0.7.3-bin-all.tgz
cd 	
```
6. Setup JAVA_HOME and SPARK_HOME
```
echo 'export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre/' >> .bashrc
echo 'export SW_HOME=/usr/local/software'
echo 'export SPARK_HOME=$SW_HOME/apache/spark'
echo 'export ZEPPELIN_HOME=$SW_HOME/apache/zeppelin'
echo 'export CONDA_HOME=$SW_HOME/conda'
echo 'export PATH=$CONDA_HOME/bin:$SPARK_HOME/bin:$SPARK_HOME/sbin:$ZEPPELIN_HOME/bin:$PATH' >> .bashrc

```
7. Copy executables

```
cp /spark-course/scripts/start_notebook.sh /usr/local/bin/
cp /spark-course/scripts/start_zeppelin.sh /usr/local/bin/
```

8. Test installation

Start-up pyspark shell
```
$SPARK_HOME/bin/pyspark
```

