# Installing a Distribution

Download the recipes and distributions

<pre>
mkdir -p $HOME/rdtk/dist && cd $HOME/rdtk/dist
git clone _to_be_determined .
</pre>

Calculate system dependencies

<pre>
$HOME/rdtk/build-generator-0.28-x86_64-linux --on-error=continue \
--cache-directory=$HOME/rdtk/gen-cache platform-requirements \
-p "ubuntu $(lsb_release -rs)" $HOME/rdtk/dist/distributions/DESIRED_DISTRIBUTION.distribution
</pre>

Generate build jobs. YOUR_API_TOKEN can be found out using the Jenkins web interface.

<pre>
$HOME/rdtk/build-generator-0.28-x86_64-linux --on-error=continue \
--cache-directory=$HOME/rdtk/gen-cache generate -m toolkit \
-D toolkit.volume=$HOME/rdtk/systems -u {YOUR_USERNAME} \
-a {YOUR_API_TOKEN} $HOME/rdtk/dist/distributions/DESIRED_DISTRIBUTION.distribution
</pre>

Open your browser, login and trigger the *-orchestration-* job.


[Back](README.md)