# Anaconda Solver Troubles
## The default solver blows!

I was struggling with this for hours. When I went to do `conda install [name
of package]`, the solver would take forever. (And it's apparently attempting
to solve an NP-complete problem too.) Well it looks like I have a fix now:

https://stackoverflow.com/questions/63734508/stuck-at-solving-environment-on-anaconda

Broadly speaking there are two suggestions that stood out: using conda-forge
packages and installing the Mamba solver. Since Miniconda already defaults to
using conda-forge, that's taken care of. All I had to do is install Mamba and
now attempting to install `jupyter-book` doesn't stall or make my craptop
hang. Problem solved, looks like.
