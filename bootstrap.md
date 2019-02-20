# Bootstrapping

Install requirements, for now Ubuntu 16.04 is supported.

<pre>
sudo apt-get install openjdk-8-jdk curl python2.7 python2.7-dev \
python-setuptools git subversion maven build-essential build-essential cmake
</pre>

Download Jenkins

<pre>
mkdir -p $HOME/rdtk/ && cd $HOME/rdtk/
wget --no-check-certificate https://ci.toolkit.cit-ec.de/job/jenkins-distribution/lastStableBuild/artifact/jenkins.tar.gz \
 -O jenkins.tar.gz
</pre>

Unzip Jenkins

<pre>
tar -xzvf jenkins.tar.gz
cd jenkins
</pre>

Create user and password

<pre>
./create_user.sh
</pre>

Start the Jenkins, you should be able to browse to https://localhost:8080

<pre>
./start_jenkins
</pre>

[Back](README.md)