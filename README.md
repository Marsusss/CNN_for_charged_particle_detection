Improvements to be made:

You should deffinatly utilize that the math is symmetric under simultaneous charge and pT inversion.
That means each image could be split in two (with a slight overlap). This would ease the training
and reduce the effect of bending lines for low pT. This modification should prolly be done
in the notebook.

In the data extraction you could change the calculations in HTTHoughTransformTool.cxx
so that the x-axis involves sin(phi0 - phi) or whatever the exact math was. The idea is
that this will force the lines to become linear, which is actually an inherent assumption
in using the CNN for the problem. This should improve the precission at the cost of making
it more problematic to produce in hardware. If you want it hardware programmable, prolly go
for a taylor approximation n see how it goes.


Data extraction.

Follow Rileys instructions. If luck favours you, you can just insert the files
under mods besides the files they correspond to. They will not be used untill the file type
is corrected. This way you can keep the modded files ready for use.

Warning: The mods might not work in the
newest Athena. Write to me at zvn474@alumni.ku.dk or marsus@live.dk. I might be able to find
an old Athena version or just help you make the mods work in the new Athena.

By enable I mean replacethe current file with my modded version with correct file type.
To just save Lm files:

enable:
HTTHoughTransformTool.cxxSaveNormal
HTTHoughTransformTool.hNormal


To save MB:

enable:
HTTHoughTransformTool.cxxSaveNormal
HTTHoughTransformTool.hNormal
HTTLogicalHitsProcessAlg.RemoveAddedMuon


If you wish to not start from the first event notice that the SkipEvents option is bugged!
Instead use the small piece of code added To:
HTTLogicalHitsProcessAlg.cxxSkipEvents
HTTLogicalHitsProcessAlg.hEventCount

The part that I modified should in general be found in between comments of "start" and "stop".
For a file to truly be enabled you should use Rileys cmake, make, source commands again.

I can see I haven't saved the run-files. But just do as Riley says. Possibly make a loop for
MB files if you like in which you remember to change the filename of the output root image
file in every iteration to not overwrite it.


root to hdf5 pd tables:
use save_hdf_clean.ipynb. Correct all paths so they point to your file and make an output
name that makes sense. Read the comments to find out what functions you need to run.


Add quick load truth:
You need to do this if you download new data from lxplus. Open Save_quick_load_truth.ipynb 
and run all. Remember to change all paths.

CNN:
Correct file names and paths to fit your data. Run initial, functions and run one of the
networks with the following functions down to training.

If you wish to train a model run stuff under training.

If you wish to load and test a model run stuff under road count and combination count.
Load either the single layer or the two layer model and remember that the network and
the loaded model must match.


