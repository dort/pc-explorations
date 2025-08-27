So this is to try to prepare for porting the codebase associated with https://github.com/Monadillo/pcn-intro from using torch to instead using JAX to see if a speedup can be accomplished.

One day after creating this specific file (my first step), i am about to rename the containing directory from yesterday's date (2025.08.26) to be project specific so I can also move the code over and begin to work directly on it.

The codebase is a jupyter/colab notebook, so in blocks, not files.

## First block is imports.

So one needs to use pip to install these packages in the venv being used to run this codebase.

torch
torchvision
tqdm
plotly
numpy

and I also noticed that in order to plot, it was necessary to additionally install the pip

nbformat


After successfully porting, the jax package should replace torch, not sure about torchvision.

tqdm shows progress which is in some sense unnecessary (I'm also not convinced keeping this as a jupyter notebook is the way to go, but happy to be talked into doing that if collaborators insist on staying within this paradigm rather than moving away to a more basic set of files)


## The 2nd block is the code that downloads and preprocesses data and builds data loaders

This is using torchvision.transforms. Claude.ai suggests that tfds and grain are options with the former being tried, true and mature and the latter being newer and less commonly used as of yet.



## The 3rd block creates the infrastructure used (predictive coding network components)

lots to change here too obviously


## Update Rules (inference and learning) are next with a Training loop and then a test loop

### Training Loop

again, lots to convert over from torch to jax

 
### Test Loop

Ditto

## setting up Plotting tools

(2 separate code blocks here)

## Model Instantiation and Training Execusion

just some parameters -- quite straightforward

### Hyperparameters for training

also quite straightforward

### Train model, store energies for plotting

just a call to train_pcn() and some printing of progress bars, then timing data when finished here, so most of the meat of our porting work gets done above

### Report Test Accuracies

as described -- quite simple -- just a call to test_pcn() and some output printed

### Plot batch-averaged energy trajectories

energy, magnitude of error, i'm still not quite clear on what the deal is with using the former label instead of the (what would seem to me to be the more accurate) latter which doesn't try to pretend something "else" is going on...

### Plot epoch averaged energy trajectories

as with the two code blocks directly above, very little to change here (just use the same stuff in a jax version, as none of it comes directly out of torch, but it's from the other libraries instead I think)
