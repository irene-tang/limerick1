# Limerick1 workspace

Technical elements of a thesis work to be submitted to the [faculty](https://www.swarthmore.edu/psychology/faculty-staff) of the [Department of Psychology](https://www.swarthmore.edu/psychology) at [Swarthmore College](swarthmore.edu) in April 2019 in partial fulfillment for the degree of Bachelor of Arts.

## Table of Contents
* [Background / Abstract [draft]](#background-/-abstract)
* [In this repository](#in-this-repository)
* [Requirements](#requirements)
* [Usage](#usage)
  * [Step 1: Gather data](#step-1-gather-data)
  * [Step 2: Generate files necessary for analysis](#step-2-generate-files-necessary-for-analysis)
  * [Step 3: Set up parameters for data analysis](#step-3-set-up-parameters-for-data-analysis)
  * [Step 4: Perform data analysis](#step-4-perform-data-analysis)
* [Support and Contributing](#support-and-contributing)
  * [Troubleshooting](#troubleshooting)
  * [Additional support](#additional-support)
* [Acknowledgements](#acknowledgements)
* [License](#license)
* [TODO](#todo)


# Background / Abstract
**_Occupation of Inner Speech in the Working Memory: <br/>
Effects of Articulatory Suppression on Anticipated Lexical Stress_**

As we silently read words on a page, we read it using an “inner voice” that includes rhythm and inflections as if we are reading aloud. We also use an inner voice when performing non-literary tasks such as problem solving, mental calculation, and decision making. Present research has not yet investigated whether these two uses of the inner voice occupy the same resources in working memory. This paper presents findings from an eye-tracking study designed to demonstrate that silent reading occupies the same working memory resources as other mental tasks. Participants read stress-alternating homographs (e.g., PREsent, preSENT) embedded in limericks, which compelled them to initially expect the incorrect prosody of the homograph and thus encountering a reading cost. In addition, participants performed articulatory suppression by repeating the word this aloud as they read. The goal of this was to see if using the actual voice would interfere with the inner voice. If so, we anticipated that the differences between reading rhythm-matching and -mismatching limericks should vanish while repeating this—thus showing that these two inner voices occupy the same working memory resource.

Key words: implicit prosody, inner voice, inner speech, subvocalization, silent reading, working memory, phonological loop, syntactic parsing, syntactic ambiguity

# In this repository

* `src/`
	* `make_new_asc/` - contains a python script that reformats the .asc data files generated by ExperimenterBuilder into one that's compatible with UMass-Amherst analysis software, which will be required to analyze our data.
		* Created by me (all blunders are mine)
		* Requires the list of subjects .py FIXME
		* Hard-coded variables: (modify these for future use)
			* input folder - FIXME here and in the script
			* `new_asc_folder` - FIXME here and in the script

	* `copy_question_acc/` - contains a python script that calculates each participant's percent accuracy on the questions, which will be required for excluding participants who were not paying attention.
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
		* Some small tweaks in variable usage were modified by me, for ease of changing their values during future replications (see hard-coded variables bullet). No changes were made to the functionality.
		* Hard-coded variables: (modify these for future use)
			* `INPUT_FOLDER` - where the new .asc files live (the compatible ones generated by make_new_asc.py)
			* `OUTPUT_FOLDER` - where the outputs regarding question accuracy will live

	* `copy_Scripter2/` - contains a perl script that generates a .script file, which will be required for make_cnt.
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
		* Some small tweaks in variable usage were modified by me, for ease of changing their values during future replications (see hard-coded variables bullet). No changes were made to the functionality.
		* Requires creating a sort of sentence file input (again, see actual instructions for details).
			* Ours is called input_to_scripter.txt. We made it by pasting stimuli into Excel, duplicating stuff, and concatenating stuff with the '^' deliminator.
			* FIXME
		* Hard-coded variables: (modify these for future use)
			* `$inputfile` - where the sentence file lives
			* `$outputfile` - where the generated .script file will live
			* `$xoff` - x offset in pixels, only if you have display change; otherwise just use return char.
			* `$yoff` - y offset in pixels, only if you have display change; otherwise just use return char.
			* `$pixrow` - number of vertical pixels per row, only if you have display change; otherwise just use return char.
			* `$sequence` - y or n depending if you want to automatically want to generate sequences

	* `copy_make_cnt/` - contains a python script that generates a .cnt file, which will be required for Robodoc.
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
		* Some small tweaks in variable usage were modified by me, for ease of changing their values during future replications (see hard-coded variables bullet). No changes were made to the functionality.
		* Requires creating a sort of parameters file
			* FIXME
		* Hard-coded variables: (modify these for future use)
			* `OUTPUT_FOLDER` - where the generated .cnt file will live
			* `input_file` - the .script file (the one generated by copy_Scripter2.pl)
			* `delim_char` - the region deliminator character in the file that was inputted to copy_Scripter2.pl
			* `lowest_cond` - the lowest condition number to be analyzed
			* `highest_cond` - the highest condition number to be analyzed

	* `copy_fix_align/` - contains an R script that performs realignment of eyetracking data, which apparently will be required for Robodoc since this is a multi-line experiment.
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
		* Some small tweaks in variable usage were modified by me, for ease of changing their values during future replications (see hard-coded variables bullet). No changes were made to the functionality.
		* Hard-coded parameters:
			* `asc_files` - where the new .asc files live (the compatible ones generated by make_new_asc.py)
			* `fa_dir` - where the fix-aligned .asc files will live (this is now v.3 of the .asc's)
			* and the rest of the parameters to the fix_align() function; see CohenBRM.pdf for details on how to set each of them
		* Non-param stuff that I changed from the original script:
			* Added a single line at the very end that calls the given fix_align() function
		* Suggestion: do not use the option to save trial plots as .tiff (i.e. set `save_trial_plots=FALSE`) unless you need them, as they will likely take up the rest of your computer's hard drive space or more, and the program already takes a while to run without it.

	* `copy_Robodoc/`
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
		* Some small tweaks in variable usage were modified by me, for ease of changing their values during future replications (see hard-coded variables bullet). No changes were made to the functionality.
		* Requires parameters file
			* FIXME
		* Hard-coded parameters:
			* `OUTPUT_FOLDER` - where the various generated files will live
			* `INPUT_FOLDER` - where the fix aligned .asc files live (the compatible ones generated by copy_fix_align.R)
		* Non-variable stuff that I changed from the original script:
			* The two or three instances of `kp.close` chaged to `kp.close()` (it was probably a typo)
			* At the end (begining from line 1021), added a loop to fix the mis-pathed entries in files_processed.lst, exclude.lst, and keep.lst (i broke the given script by switching it to INPUT/OUTPUT from outside the current directory)
				<!-- * Also append a newline before  each of these files, since eyedry seemed to be skipping the first line (probably assumed there was a header there--but there isnt') -->
	* `copy_dataanal_714` - contains a bunch of analysis software.
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
			* ANALASC.doc seems to be the README equivalent for the folder
		* We are only interested in `eyedry` in particular, hence the seprate `eyedry/` folder (described right below)
		* Each comes with a pre-compiled .exe executable that can only be run from Windows Command Prompt, but the C code can compiled with any compiler (we used GCC) on any Mac/Linux/Windows bash terminal.
		* Nothing is done with this folder besides archiving its contents
	* `eyedry/` - contains the analysis software that we use.
		* Created by the UMass-Amherst Eyetracking Lab. See the actual instructions and documentation in this subfolder for details.
		* Instructions for analysis are below in the Usage section.

* `data/`
	* `FA_Dir/`
		* contents are auto-generated by fix_align
	* `new_asc/`
		* contents are auto-generated by new_asc
	* `original_asc/`
		* put original .asc data here by hand
	* `question_acc/`
		* contents are auto-generated by question_acc
	* `robodoc/`
		* contents are auto-generated by robodoc
	* `scripter/`
		* contents are auto-generated by scripter and make_cnt
	* `eyedry/`
		* FIXME

* `test/`
	* everything in here is archived junk

* a mountain of technical difficulties

# Requirements

* [python3.4+](https://www.python.org/downloads/)
* [perl](https://www.perl.org/get.html)
* [R](https://www.r-project.org)
* [GCC compiler for C](https://gcc.gnu.org/releases.html)

This package works with Mac and Linux terminals. It works with Windows too, but only with the Command Prompt (CMD) (not Bash, since it'll a pain to retrieve generated files). However, CMD uses different commands than the ones described in the usage instructions below, and when you do something wrong whilst running eyedry it crashes without showing you the error message.

TL;DR: Best to use macOS or Linux.

# Usage

## Step 1: Gather data
1. **Create the experiment in ExperimentBuilder.**
	* Ideally, we would have create it using the UMass eyetracking experiment template to avoid the technical struggles of getting to data analysis, but we could not with this particular experiment because this experiment has a secondary task component that isn't supported by the UMass setup.
2. **Run participants.**
	* Experimenter script, debriefing, participant log, pre-registration, etc. are located in the `EyeTrackingLabAdmin/Limerick1/` shared Drive folder.
	* Information about how stuff was run and where files are located can be found in the Experimenter Script.
3. **Convert data files from EDF to ASC**
	* Each participant's data will be located on the Host computer in e.g. `Desktop/Exeriments/LimerickProsodyDeployed/LimerickProsodyA/results/subject0/`
	*  In that folder, there should be an .edf file titled e.g. `subject0.edf`.  Double-click on that .edf file to generate an .asc file.
		*  There's some EDF to ASC converter software installed on the Host computer that allows it to do that.  Double-clicking an EDF file on your personal computer won't do anything if you don't have that software installed.
4. **Gather original ASC files and AOI folders**
	* Once the .asc file has been generated, copy it onto a thumbdrive or  something and place it into this package's `data/original_asc/` folder.
	* Also copy each of the eight Areas of Interest (AOI) folders into this package's `data/original_asc/` folder, so that it contains `A_aoi/`, `B_aoi/`, `C_aoi/`, `D_aoi/`, `RevA_aoi/`, `RevB_aoi/`, `RevC_aoi/`, `RevD_aoi/`.
5. **Match participants with their list**
	* This experiment used a Latin Square design. Participants saw one of eight possible lists. Analysis will require knowing which list each participant saw.
	* In `src/make_new_asc/lists.py` is a dictionary mapping lists to participants who saw that list. The eight lists are A, B, C, D, RevA, RevB, RevC, RevD.

## Step 2: Generate files necessary for analysis
From within the `/src` directory, run:
```
python3 runall.py
```

All input variables are already written into the respective scripts (but see above section for where to modify things during future use). This single script executes the following all at once in this order:

* Deletes all subfolders (and their contents) except for original_asc/ and eyedry/, and then recreates them as empty folders for a fresh start
* make_new_asc.py
* copy_question_acc.py
* remove_participants_question_acc.py
* copy_Scripter2.pl
* copy_make_cnt.py
* copy_fix_align_v0p92.R
* copy_Robodoc.py

## Step 3: Set up parameters for data analysis

1. From within `src/eyedry/`, compile eyedry: (ignore any warnings)
```
gcc eyedry.c -o eyedry
```

2. From within `src/`, run the executable that we just created:
```
./eyedry/eyedry
```

3. Eyedry will ask a series of questions. Answer as follows:

Question | Answer
-------------------------------------------------------:|:-------------------------
What is the output trace file name? | trace_1.txt (or whatever)
Type an identifying string to print out |whatever
What is the maximum number of fixations on an item |press return
Type name of file containing control info (CR if none) |`eyedry/limerick1.ctl`, or press return and re-generate it as follows:
Debug level |0
Do you want to eliminate trials... |n
Do you want to eliminate trials... |n
What is the smallest numbered experimental item? |1
largest |40
How many regions maximum? |7
What is the smallest condition number... |1
largest |4
subconditions |put 4 even though I have no idea why, it breaks otherwise
What field is the condition number in |2
What field is the item number in |3
What field is the number-of-fixations number in |6 ***** this is different than suggested in the aged manual; see HowToReadRobodocOutput documentation for how to read .da1 file
What field do the data start in? |7 ***** same difference as above
Longest fixation time |9000
Shortest |1
screen width |160 (I hope)
max number of lines |5
d |n
d |y?
d |n
d |n

4. On the screen where it asks to confirm the entered values, double-check them and correct errors if necessary, then press return to continue.

5. Answer as follows:

Question | Answer
|---|---|
What is the name of file that lists data files? |../data/robodoc/keep.lst
Any exceptions file? |n
~~Control~~ Count (.CNT) file name?    |../data/scripter/output_from_scripter.cnt

5. The next step should be "Which analysis?" with a list of possible analyses to perform. If this is true, continue to the next step. If not, something probably went wrong.

## Step 4: Perform data analysis
Stuff that Breen & Clifton (2010) did:

* Prior to analysis:
	* Eye movement data was cleaned of track losses, blinks, and long fixatios over 800ms using EyeDoctor.
	* Short fixations (<80ms) were incorporated into the nearest neighboring fixation within three characters, otherwise deleted
	* Long fixations (>800ms) were deleted
	* Trials with blinks or track losses on the critical word were eliminated

* Standard eyetracking measures, following Rayner (1998) and Rayner et al. (1989)
	* **First-pass time** - sum of all fixations made from first entering to first leaving a region, eliminating trials on which no such fixations occurred
	* **Go-past time** - sum of all fixation durations made from first entering a region to first leaving it to the right
	* **Probability of fixating in a region** - no description provided
	* **Probability of regressing out of a region given that it was  fixated during the first pass**  - no description providd
	* First fixation duration for critical Region 3 (but there was no significance here so these data are not reported)

NOTE: the program segfaults. either if choosing "y" for "do you want info aboutlong and short times printed" or if trying to get files formatted for Systat, or both.

* Notes
	* First pass time
		* Throw away zero fixation? y - since eliminating trials on which no such fixations occurred
		* Do you want to culiminate or average? a
		* RAW times, MS/char, or DEVIATION from regression: r
		* Conditionalize on presence/absense of regression in critical region? n
		* Conditionalize on presence/absense of fixation in critical region? n
		* What is the upper summed cutoff for first pass time? default
		* COnditionalize on position of the last fixation before each region? n
		* file of item X subject combinations
			* do you want all .. a
			* wide or narrow .. w
		* subject by subject file
		* item by item file
		* do you want information about long and short times, n



Check that the analyses are actully working (check by hand)
* Compare them the video viewer in ExperimentBuilder, play the videos at 25% of the speed
* somehow match them back together:
	* Note: the TRIALID for the original .asc  and the Dataview are off-by-one; .asc starts at 0 while Dataviewer starts at 1
	* the sequence  should correspond to the dataview trialid with this relationship: dataviewer_trialid = (sequence +  1)/2 + 1 becuase of math
	* double-check: for an IXS data file, check the item number (3rd  column) with the input_to_scripter in Excel;  they should  be the same limerick, as with  checking against the original asc
	* triple-check: the condition number should match against the original asc
* checking using Prob of Fixation didn't seem that helpful since most  cooperative participants fixated in every region  anyways so it was mostly 100% and even the ones where the data program predicted 0% the participant  still showed fixations so  it  was hard to tell whether they actually matched up
* checking using Gopast time -  inprogress

Get the analysis files, then see the trace.txt file for a trace of how we go there

# Support and Contributing

## Troubleshooting

* Help I lost a data file
	* Copies of every .edf should be stored on the Source computer

## Additional support
* If anything is buggy or unclear, please open an issue or pull request, or contact ~~itang1@swarthmore.edu~~ itang1@alumni.swarthmore.edu.
* This repo is no longer actively being maintained as of May 2019.

# Acknowledgements
Thanks to Professor [Dan Grodner](https://www.swarthmore.edu/psychology/faculty-staff) for enormous guidance and so much invested time over the years; to Professors [Dan Grodner](https://www.swarthmore.edu/psychology/faculty-staff) and [Nathan Sanders](http://sanders.phonologist.org) for setting up the experiment; to Drs. [Mara Breen](https://www.mtholyoke.edu/~mbreen/) and [Charles Clifton](http://www.umass.edu/pbs/people/charles-clifton) for providing the [stimuli](https://www.mtholyoke.edu/~mbreen/pubs/LimericksItems.pdf) and [research](https://www.mtholyoke.edu/~mbreen/pubs/BreenClifton_JML_2011.pdf) on which this study was based; to Drs. [Charles Clifton](http://www.umass.edu/pbs/people/charles-clifton), [Adrian Staub](https://www.umass.edu/pbs/people/adrian-staub), [Andrew Cohen](https://www.umass.edu/pbs/people/andrew-cohen), [Jesse Harris](https://linguistics.ucla.edu/person/jesse-harris/), and [colleagues](http://blogs.umass.edu/eyelab/people/) for creating and maintaining the [eyetracking analysis software](http://blogs.umass.edu/eyelab/software/) that we relied so heavily on; to the alumni and current students practicing research in the [Swarthmore Psycholinguistics Lab](https://www.swarthmore.edu/psychology/labs); to the [Swarthmore Department of Psychology](https://www.swarthmore.edu/psychology) for sponsoring the experiment, and to the undergraduate students at [Swarthmore College](https://www.swarthmore.edu) who participated in the study.

# License
[MIT License](https://github.com/itang1/limerick1/blob/master/LICENSE)

(c) Copyright 2019 Swarthmore Psycholinguistics Lab etc.

This project was created for non-monetary educational purposes only (please don't sue me)


# TODO
* create rest of the analysis files
<br/><br/>
* make this readme less awful
* finish the readme for the rest of the drive folder
* still writing the actual paper
* will there be a part 2
* (unrelated) make progress on the other scalar judgement loading study replication