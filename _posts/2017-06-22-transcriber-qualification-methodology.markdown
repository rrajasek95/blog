---
title: CMUSphinx GSOC 2017 - Pronuncation Evaluation Methodology
layout: post
categories: gsoc
---

In this project, the overall goal is to create an automated mechanism to evaluate the intelligibility of the speech of non-native English speakers and use that as an educational aid to improve the speaker's diction. A high level workflow of the system can be described as follows:
- Have the user make a recording of a prompted phrase on their device. A simple example would be "What is your name?", which is read out by the user into the microphone. Alternatively, he could upload a recording of whatever he spoke as an mp3 or WAV.
- Have an analysis system either on the client or the server side accept the recording as input and process it.
- The analysis system then verifies whether the spoken recording is pronounced correctly. If the user has made a mistake, have the system indicate where the user has made an error and give the correct pronunciation to them so that they can rectify it.

In the above workflow, the user's speech is evaluated in a manner that takes into account different speaker accents, pace of speech and whether the user said the correct phrase. Therefore, we need an evaluation system that is flexible enough to account for the aforementioned issues and at the same time, provide an accurate evaluation of the speech.

{% cite loukina %} from ETS describe a method of quantifying the intelligibility of an ESL (English as Second Language) speaker which involves segmenting recorded speech into short phrases. The recordings are in response to prompt phrases or questions which are presented to the speaker. These phrases are then presented to transcriptionists who attempt to transcribe the recorded phrase. The transcriptions were then aggregated and compared against the original prompt. A group of annotators were then given a set of recordings and their corresponding transcripts and were asked to mark whether the words in the transcript were intelligible. ETS then devised a multi-level model which correlated the pronunciation and intelligibililty of the speaker to derive a metric for evaluating speaker proficiency.

The pronunciation evaluation model that we're designing is based partly on this approach. It splits the prompt phrase into a set of phonemes, based on a user defined grammar. The PocketSphinx pronunciation evaluation module processes the recording and generates acoustic scores for each phoneme. The scores are grouped based on the word the phoneme is part of and a trained classifier takes these scores as inputs and designates the given word as intelligible or unintelligible, which is then highlighted to the user as requiring correction.

The main component of the model is the classifier. As mentioned, it takes word level scores obtained from the pronunciation evaluation module and some other data as input and outputs a `1` if the given word is intelligible and `0` if the word is unintelligible. The input features are the acoustic scores normalized by logarithms and the duration of each phoneme as well as the phoneme recognized in place of the correct phoneme. The classifier can be modelled using simpler linear models such as Logistic Regression or deep architectures. The main trade-offs will be on accuracy versus the time, complexity and data requirements for training a robust model.

We will adapt ETS' approach by incorporating the recording and transcript collection tasks, with the scoring task being automated using PocketSphinx. [My previous post]({{page.previous.url}}) provides a brief overview of the work that I will be doing. I'll describe the system in more detail and provide progress of the data collection task in the upcoming blog posts. So until then, stay tuned for more!


References
----------
{% bibliography --cited %}

