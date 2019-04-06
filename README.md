This repository contains two notebooks, which you can open here on GitHub to quickly see the results:
- `CPS.ipynb`
- `Census.ipynb`

The `.csv` files contain the tables produced by these two notebooks. Below I paste instructions on how to get these notebooks running on a (linux) server.

# Installing Anaconda
Or Miniconda, to be precise. We just follow the steps [here](https://gist.github.com/arose13/fcc1d2d5ad67503ba9842ea64f6bac35):
```bash
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
rm ./Miniconda3-latest-Linux-x86_64.sh
```

Due to some strange bug in miniconda installation, `PATH` is not set correctly. To fix this, execute
```
nano ~/.bash_profile
```

and make sure that it contains 
```
PATH=$PATH:$HOME/miniconda3/bin
```
So basically change `miniconda` to `miniconda3`. Log out, log in and you are ready to `conda` :)

A handy thing is to add `conda-forge` to conda channels, since a lot of packages are availible through it (so we can aviod `pip`):
```
conda config --add channels conda-forge 
```

## Creating conda environments

Using environments is recommended (for replicability, important if you do your work across multiple machines), and conda makes using them easy. Miniconda will not install any packages (not even python) by default, so to start working, let's create an environment called `main` and install `pandas`, `jupyterlab`, `seabord` and `requests` (which also install the required dependencies):

```
conda create -n main pandas jupyterlab seaborn requests
```
Once this is done, we activate the environment with
```
source activate main
```
and when we want to leave it we just enter
```
source deactivate
```

Here's how to install packages: first, activate your environment (as shown above). Then, if we want to, for example, install `scipy`, do:
```
conda install scipy
```

## Using jupyter notebooks

Of course we won't be actually using python from the console, so let's show how to use Jupyter Notebooks - to be specific, we'll use something even better, Jupyter Lab (which we already installed in our environment `main`). So, on the server, we first `cd` to the directory we want to work with, activate our environment, and then execute
```
jupyter lab --port=9000 --no-browser
```
Then, on our local computer (assuming it is a linux or mac) we execute
```
ssh -N -f -L 9000:localhost:9000 <USER>@<SERVER NAME>.mit.edu
```
And that's it, we can work!
