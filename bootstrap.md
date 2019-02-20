# Bootstrapping

<pre>
sudo apt-get install openjdk-8-jdk curl python2.7 python2.7-dev \
python-setuptools git subversion maven build-essential build-essential cmake
</pre>

<pre>
mkdir -p $HOME/rdtk/ && cd $HOME/rdtk/
wget --no-check-certificate https://ci.toolkit.cit-ec.de/job/jenkins-distribution/lastStableBuild/artifact/jenkins.tar.gz \
 -O jenkins.tar.gz
</pre>

<pre>
tar -xzvf jenkins.tar.gz
cd jenkins
</pre>

<pre>
./create_user.sh
</pre>

<pre>
./start_jenkins
</pre>