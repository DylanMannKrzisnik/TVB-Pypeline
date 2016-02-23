# TVB-Pypeline - - Work in Progress!

This project maps our current automatized MRI processing pipeline (http://github.com/BrainModes/TVB-empirical-data-pipeline) 
to Python using Nipype, making the used toolboxes inside easily exchangeable.

For a general overview about the pipeline see [Schirner, Rothmeier et al. (2015)](http://www.sciencedirect.com/science/article/pii/S1053811915002505)

----------

## Installation:
The Pipeline uses Nipype which depends mainly on **Python 2.7**. The following list gives an overview about the Python toolboxes which are used in the current state of the Pipeline. See the corresponding Doc-Pages for installation and dependency resolving.
+ [Nipype](http://nipy.org/nipype/users/install.html)
+ [Nibabel](http://nipy.org/nibabel/installation.html#installation)
+ [Dipy](http://nipy.org/dipy/installation.html)

Since Nipype/Python also perform as a wrapper for Toolboxes invoked through the Shell-Interface, you also have to make sure the toolboxes you want to use are installed on your system and their binaries/libs are included in the Shell's searchpath.

For **preprocessing**, the following toolboxes are used:
+ [FSL](http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/)
+ [FREESURFER](https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall)

When it comes to **fiber tractography**, there is a vast number of available tools for that. Their usage also highly depens on how your dwMRI-Data was recorded. One of the main parting points is the number of different diffusion-gradient strengths applied during the measurement (i.e. the number of different **b-values**). If the dataset has only a single value greater than zero, one talks about **single-shell data**. As soon as more than one value (>0) is involved, the data is called **multi-shell data**

To run it on a specific cluster architecture, simply edit the plugin-type in the master control script

----------

## TODO-List:
+ ~~Write a new Documentation!~~
+ ~~Implement fMRI processing based on the code here: https://github.com/BrainModes/TVB-empirical-data-pipeline/blob/NSG/fmriFC.sh~~
+ Implement Tractography Thresholding into the MRTrix module. Possibly trying to include the method described in [Morris et al. (2008)](http://www.sciencedirect.com/science/article/pii/S1053811908007301). Alternatively one could also dig up the old hard-threshold code since the short-range tracking-flares are rendered meaningles anyway by our aggregation method!
+ Make the file-sorting of the user-data more sophisticated. This means that the pipeline should be able to somehow recognize which kinds of data-sets (e.g. fMRI, T1, dwMRI) is included in the user data and then route the particular folder-paths onto the corresponding processing-nodes inside the pipeline. This might be achieved through using nipype's [SelectFiles interface](http://nipy.org/nipype/users/select_files.html)
+ Include some example workflows for different cluster scenarios, realized through e.g. controll-scripts written in BASH
+ Re-Implement Multishell-Tracking using FSLs bedpostx as in https://github.com/BrainModes/TVB-empirical-data-pipeline/tree/multiShell
