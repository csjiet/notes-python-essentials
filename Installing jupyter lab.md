1. pip install anaconda 
2. conda install jupyterlab
3. nbextensions
	1. conda install -c conda-forge jupyter_contrib_nbextensions 
	2. conda install -c conda-forge jupyter_nbextensions_configurator
	3. jupyter contrib nbextension install --user
4. conda install ipywidgets (to resolve: Uncaught exception GET /api/nbconvert)
5. conda install ipykernels
6. $ echo "alias pip=/usr/local/bin/pip3" >> ~/.bash_profile (to fix no module: ipykernel_launcher)[source1](https://stackoverflow.com/questions/57422648/no-module-named-ipykernel-launcher)[source2](https://opensource.com/article/19/5/python-3-default-mac#what-to-do)
