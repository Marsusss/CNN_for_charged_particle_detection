Improvements to be made:

You should deffinatly utilize that the math is symmetric under simultaneous charge and phi0 inversion. (Except for the constant shift inside the equation I suppose, but that doesn't matter for this execise, that'd be up to someone else to make sure we get the right coordinates out for both positive and negative charge, just state that it obvious that we can as long as we remember which ones we inverted. This is also only unproblematic for our exercise because it is an inherent assumption in our model (the CNN) that the images can be interpreted equally everywhere, which is admitedly only halfway true for low pT's due to the sine. But all the same, we allready assumed it, so it shouldn't hurt the model efficiency I think and has all the advantages listed below.)
That means each image could be split in two (one for positive charge and one for negative with a slight
overlap). That could be interpreted equally. This would ease the training and reduce the effect of
bending lines for low pT. And double the amount of events for training in approximately the same time. This modification should prolly be done in the notebook.
Edit: I implemented a "get_smart_image" function for this in the CNN. You can use that. You still need to edit other places to make sure that the new number of events and size of the qOpT-dimension fits in other places.

In the data extraction you could change the calculations in HTTHoughTransformTool.cxx
so that the y-axis involves asin(q/pT) or whatever the exact math was. After thinking
long and hard I decided we prolly can't add the sine to the x-axis, i.e. sin(phi0 - phii)
as phii (along with ri) is what seperates them. You'd just get a lot of lines on top of each
other I think. The idea is that this will force the lines to become linear, which is
actually an inherent assumption in using the CNN for the problem. This should improve the
precission at the cost of making it more problematic to produce in hardware. If you want it
hardware programmable, prolly go for a taylor approximation n see how it goes.

I used a modfied version of the CAM-method to show what patterns the network was looking for.
This could have been done better by modifying the current final layer to mapping to more
channels than 2 and then making the two output channels a mean of these. Adding an "average" layer you can say. Then you can modify
the current method to taking the channels before the averaging out. See 
http://cnnlocalization.csail.mit.edu/Zhou_Learning_Deep_Features_CVPR_2016_paper.pdf and my
thesis or just ask me. This is a great way to illustrate the effect of a CNN so would be great
for your presentation.



Data extraction.

Follow Rileys instructions. If luck favours you, you can just insert the files
under mods besides the files they correspond to. They will not be used untill the file type
is corrected. This way you can keep the modded files ready for use.

Warning: The mods might not (= almost certainly won't) work in the
newest Athena. Write to me at zvn474@alumni.ku.dk or marsus@live.dk in this case. I might be able to find
an old Athena version or just help you make the mods work in the new Athena.

By enable I mean replace the current file with my modded version with correct file type.
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


