## Automated Builds 

Available at: TODO

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
