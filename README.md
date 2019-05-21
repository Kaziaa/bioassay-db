# bioassay-db
Workflow for generating db from PubChem bioassay 

## Server set-up
* Set up mini-conda
  * download and install miniconda https://docs.conda.io/en/latest/miniconda.html, choose yes to add it to .bashrc
  * conda create -n bioassay
  * conda activate bioassay
  * conda install jupyter notebook numpy pandas matplotlib tqdm psycopg2 sqlalchemy
  * conda install -c openbabel openbabel
  * conda clean -a
* Set up jupyter notebook
  * jupyter notebook --generate-config
  * to set-up remote access edit ~/.jupyter/jupyter_notebook_config.py
    * c.NotebookApp.allow_remote_access = True
	* c.NotebookApp.ip = '*'
	* c.NotebookApp.open_browser = False
	* c.NotebookApp.password = 'sha1:...'
    * c.NotebookApp.port = 8080
* Set up jupyter lab (optional)
  * conda install -c conda-forge jupyterlab
  * conda install -c conda-forge nodejs
  * jupyter labextension install @jupyter-widgets/jupyterlab-manager
* Set up rdkit & postgres (though not using rdkit at the moment)
  * conda install -c rdkit rdkit rdkit-postgresql
  * apt-get install libfontconfig1 libxrender1
  * adduser postgres
  * su - postgres
  * <path to miniconda3>/bin/conda init bash
  * exit
  * su - postgres
  * conda activate bioassay
  * initdb -D <path-to-db>/postgresdb
  * pg_ctl start -D <path-to-db>/postgresdb -l <path-to-db>/postgresdb/log
  * psql postgres
  * \password postgres
  * create extension rdkit;
  * \q
  * TODO: setup postgres as a service to start on boot
* finally run 'jupyter notebook' or 'jupyter lab'
