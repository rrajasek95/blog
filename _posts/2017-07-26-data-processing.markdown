---
title: CMUSphinx GSOC 2017 - Data Processing
layout: post
comments: true
---

# Prelude: A Confession and a Promise

There's this rather bad habit that I have which I need to sort of amend, which is that of not regularly updating on my progress. It's one aspect of GSoC that I haven't been putting enough effort into despite it being a crucial aspect of Summer of Code work. Even though I've been making constant progress in my GSoC work (of which there has been a major change, more details on that in the next blog post), a lot of people in the org have been in the dark about the work I've been doing. So here's a formal pledge to keep updating on my progress on a regular basis. 

A very crucial aspect of fixing this habit is actively forcing myself to adhere to a strict routine and making use of tools and techniques. I'm going to schedule my blog posts so that I can pace my progress on the coding work.

Anyways, now that's out of the way, let's move straight to the work

# Procesing the data
As part of the data collection task, we've collected recordings for several words and phrases and the transcripts for each of those recordings. To score the recordings, we make use of the PocketSphinx pronunciation evaluation, for which the usage is documented [here](https://cmusphinx.github.io/wiki/pocketsphinx_pronunciation_evaluation/).

Now, we have several groups of recordings (based on the utterance) that we need to perform this processing step for. As a result, I simplify part of my task by grouping the audio files into folders named after the recording. The dataset I had access to had over 800 words and 2400 sentences in English spoken by Chinese students.

For performing the pronunciation evaluation, we require the audio to be sampled at 16000Hz with 16 bits per sample and 1 monophonic channel. For this, I use the utility `mpg123` which converts the MP3 to the corresponding WAV format.

I use it as a function in my bash scripts to mass convert by performing a `find` on any MP3s and output the wav in the same directory. The process is reasonably fast since the recordings are quite brief.

```
function f_mp3towav {
    mpg123 -w $2 $1
}
```

After converting the recordings, we require to perform an alignment using a grammar for each word/sentence. To produce the grammar files, we require a standardized set of pronunciations for a set of English words. Thankfully, we can obtain this by parsing [CMUDict](http://www.speech.cs.cmu.edu/cgi-bin/cmudict) for the pronunciation of common words. [This gist](https://gist.github.com/rrajasek95/8355070a870d5eea94f4c3fce210168d#file-create-subset-dict-py) shows the process for generating the subset of the dictionary that we're gonna use. We assume that the files are stored in folders named after the utterance. The code involves some manual segmentation of certain words and handling of punctuation which is specific to the folder structure that I've used.

The process of generating the JSGF is quite simply:

```
import sys

import os
folder_list = set(os.listdir("words"))

with open('subset_words.dict', 'r') as f:
    for line in f:
        tokens = line.strip().lower().split(maxsplit=1)
        if tokens[0] not in folder_list:
            continue
        with open('words/{0}/{0}-align.jsgf'.format(tokens[0]), 'w') as w:
            w.write('#JSGF V1.0;\ngrammar forcing;\npublic <{}> = sil {} [ sil ];\n'.format(tokens[0], tokens[1]))
```

The case for sentence is analogous for sentences where we string all the phonemes for each word in sequence. The code for that is in [this gist](https://gist.github.com/rrajasek95/8355070a870d5eea94f4c3fce210168d#file-create-sentence-jsgf-py).

We then run the forced aligner on this grammar to obtain the acoustic scores and duration of the phoneme for each word in the sentence. This is pretty much identical to the method listed in the tutorial above and I created a function for this

```
function f_force_align {
    audio=$1
    align_jsgf=$2
    phoneme_dict=$3
    echo $audo
    pocketsphinx_continuous -infile $audio -jsgf $align_jsgf -dict $phoneme_dict -backtrace yes -fsgusefiller no -bestpath no -wbeam 1e-56 -beam 1e-57 2>&1 | tee $audio"-align.txt"
}
```

Note that there may be certain recordings where the aligner may throw a grammer error. Adjusting the beam parameters in this case should fix that.

From these alignments, we can obtain the acoustic scores for each word. We'll obtain statistics for the data by following the procedure listed in the CMUSphinx tutorial to obtain the lognormal acoustic scores (as I've done with [this script](https://gist.github.com/rrajasek95/8355070a870d5eea94f4c3fce210168d#file-create-normalign-sh)). We then make use of the above score data as a feature for evaluating intelligibility of the utterance.

I'll be covering the processing of the transcripts in the next blog post in more detail as well as the methodology for building the model for intelligibility in the next blog post. The overall gist for this code can be found [here](https://gist.github.com/rrajasek95/8355070a870d5eea94f4c3fce210168d) which contains the majority of scripts that I've used for recording preprocessing. So until then, stay tuned for more!

P.S. I've added a Disqus comment field, so I urge you to share your feedback and ideas to improve my content.