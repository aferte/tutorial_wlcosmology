# Tutorial KIPAC WL Cosmology

Tutorial for KIPAC on cosmological inference with 3x2pt: analyze a simulated LSST Y10 3x2pt data vector (with SRD specificities) in LCDM using CosmoSIS.  

Instructions to run a full chain on sherlock:

1. Connect to sherlock. I recommend working in $SCRATCH or in your space in $OAK.

2. Install cosmosis environment and get cosmosis-standard-library by running the following commands:
   
The following takes a while so we request an interactive node:
> sh_dev

The conda install does not work (it used to, at least until this summer - strange!). Joe recommends the following which I have not tested on sherlock:

> conda install -c conda-forge mamba
 
> mamba install -c conda-forge cosmosis cosmosis-build-standard-library

Otherwise, we follow the instructions from https://cosmosis.readthedocs.io/en/latest/intro/installation.html#conda-forge-from-scratch which works well, although time consuming:

> wget -O Miniforge3.sh  https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh

> chmod +x Miniforge3.sh

> ./Miniforge3.sh -b -p ./env_cosmosis

> source ./env_cosmosis/bin/activate

> conda install -y cosmosis cosmosis-build-standard-library

> source cosmosis-configure

> cosmosis-build-standard-library main

Now you have the cosmosis environment which you can activate by doing
> conda activate ./env_cosmosis

> source cosmosis-configure

and you have cosmosis-standard-library that has all CosmoSIS modules.

3. Add needed package for nautilus:

After activating the CosmoSIS environment, do:
> pip install h5py 

3. Wherever you want (e.g. $SCRATCH), clone this github repository:
> git clone git@github.com:aferte/tutorial_wlcosmology.git

4. Edit the job submission script:
> cd tutorial_wlcosmogy/ini_inference

> emacs -nw lssty10_32pt_run.sh

Edit the file to set the cosmosis environment and the location of your cosmosis-standard-library.
Save and exit the file.
You can give your stanford email address in the header of the sh file to receive notifications about your job, they get to your stanford inbox but not forwarded to your SLAC inbox :(

5. Submit the chain by running (exit sh_dev if you are still on the interactive node):
> sbatch lssty10_32pt_run.sh

This will run a chain on 200 CPUs for a few hours, it will write the chain in chain_lssty10_32pt_srd_nautilus.txt in tutorial_wlcosmogy/ini_inference.
To get contour plots, use tutorial_wlcosmogy/script_plot/plot_chain.py !!You need to edit line 134 to point to the correct chain's path!!

Happy chain running!

 
