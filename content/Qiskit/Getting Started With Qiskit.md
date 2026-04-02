---
title: Getting Started With Qiskit (A Setup Guide For LazyVim)
---
Qiskit is an open source, python based software stack developed by IBM for quantum computing (QC). It is a wonderful tool for learning about QC, and I would highly suggest experimenting with it in your editor of choice. 

I am using neovim (with LazyVim) on Linux, so my setup guide will of course be tailored to that, as I cannot speak for much else. If you are using a different editor or OS, please refer to the [official documentation](https://github.com/Qiskit/qiskit).

***

### Setup Guide 

If you already have nvim working on your system, you can begin following the LazyVim [installation guide](https://www.lazyvim.org/installation), which has instructions for Linux, MacOS, and Windows. It is perfectly fine to clone the starter configuration and work from there. This is exactly what I did. 

Next, you will need to install `lang.python` and `neo-trees` in LazyExtras. To do this, run
```
:LazyExtras
```
and search for those extras in the long list that (hopefully) pops up. If you're not already familiar with nvim, the `/` key enables you to search for things. 

I would strongly suggest installing qiskit in a virtual environment, rather than in your system python (now is also a good time to check that you have python installed, if you haven't already). To set up the virtual environment, run
```
python3 -m venv ~/venvs/qiskit
source ~/.venvs/qiskit/bin/activate
pip install qiskit ipykernel
```
*Note: I enter this virtual environment via the terminal before opening nvim each time by typing `source ~/.venvs/qiskit/bin/activate`. If this is successful, you will see `(qiskit)` before your user. Then, you can type `nvim` and you will be ready to go.*

Now, for the moment of truth, create and open a test python file:
```
nvim test_qiskit.py
```
Type some sample code in this new python file for now, in order to test that Qiskit is functional:
```
import qiskit
print(qiskit.__version__)
```

My setup at the moment, and I am sure this is not ideal, is to create a vertically-split display. In normal mode, type `:split` and open a terminal in one of the windows with `:terminal`. 

In the terminal, you can run this python file by typing:
```
python test_qiskit.py
```
*Note: You may set up a keybind to automate this, so you don't have to type this into the terminal every time you want to execute your code, but I have not done this yet.*

If qiskit was properly installed and imported, you should see in the terminal the version of qiskit outputted. 

If this works for you, **congratulations!** You have successfully set up qiskit and you are ready to start experimenting with it! If you are completely inexperienced with qiskit, I would suggest going through the [[Resources|Demo Projects]] section next!