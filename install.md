# Installing a Distribution

<pre>
mkdir -p $HOME/rdtk/dist && cd $HOME/rdtk/dist
git clone TODO .
</pre>

<pre>
$HOME/rdtk/jenkins/job-configurator --on-error=continue \
--cache-directory=$HOME/rdtk/gen-cache platform-requirements \
-p "ubuntu $(lsb_release -rs)" $HOME/rdtk/dist/distributions/DESIRED_DISTRIBUTION.distribution
</pre>

<pre>
$HOME/rdtk/jenkins/job-configurator --on-error=continue \
--cache-directory=$HOME/rdtk/gen-cache generate -m toolkit \
-D toolkit.volume=$HOME/rdtk/systems -u {YOUR_USERNAME} \
-a {YOUR_API_TOKEN} $HOME/rdtk/dist/distributions/DESIRED_DISTRIBUTION.distribution
</pre>

Open your browser, login and trigger the *-orchestration-* job.