## Automated Builds

Available at: https://rdtk.github.io/documentation/index.html

## Manual

### Build

<pre>
  pip install -U sphinx --user
  pip install sphinx_rtd_theme --user
  git clone https://github.com/RDTK/documentation.git
  cd documentation
  make html
</pre>

### Delpoy

From master branch run:
<pre>
  make gh-pages
</pre>

## Acknowledgments

The development of this software has been supported as follows:

- The development of this software was supported by CoR-Lab, Research Institute for Cognition and Robotics Bielefeld University.
- This work was supported by the Cluster of Excellence Cognitive Interaction Technology ‘CITEC’ (EXC 277) at Bielefeld University, which is funded by the German Research Foundation (DFG).
