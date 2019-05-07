# Bootstrapping

Install requirements, for now Ubuntu 16.04 is supported.

<pre>
sudo apt-get install openjdk-8-jdk curl python2.7 python2.7-dev \
python-setuptools git subversion maven build-essential build-essential cmake
</pre>

Download Generator

<pre>
mkdir -p $HOME/rdtk/ && cd $HOME/rdtk/
wget https://github.com/RDTK/generator/releases/download/release-0.28/build-generator-0.28-x86_64-linux
chmod +x build-generator-0.28-x86_64-linux
</pre>

Install Jenkins
<pre>
./build-generator-0.28-x86_64-linux install-jenkins jenkins
</pre>


Create user
<pre>
./build-generator-0.28-x86_64-linux create-jenkins-user  --username=USER --password=PASS --email=MAIL jenkins  
</pre>

Start the Jenkins, you should be able to browse to https://localhost:8080

<pre>
jenkins/start_jenkins
</pre>

[Back](README.md)