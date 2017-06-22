---
title: CMUSphinx GSoC 2017 Project Overview - Transcriber Qualification
layout: post
categories: gsoc
---

# Background
CMUSphinx is one of the most active open source communities providing state of the art tools for speech recognition. The project's site can be found [here](https://cmusphinx.github.io/) and the Github repository [here](https://github.com/cmusphinx). I got to find out about CMUSphinx when doing research about my final year project on forced transcript alignment. It gave me access to a lot of useful material and some crucial insights about it which helped towards my final project. Finding out that it was one of the Google Summer of Code selected organizations this year was pleasant news to me, hence leading me to apply to it. 

I am working on the project _[Transcriber Qualification](https://summerofcode.withgoogle.com/projects/#6044456057831424)_, whose goal is to act as a support to two other projects -- _[Pronunciation Intelligibility Remediation](https://summerofcode.withgoogle.com/projects/#6205453974372352)_ by Brij (whose blog you can check out [here](https://pronunce.blogspot.in/)) and _[Computer Assisted Learning Including Speaking Skills](https://summerofcode.withgoogle.com/projects/#5526592114655232)_ by Sahith Dambekodi (who posted to the CMUSphinx blog [here](https://cmusphinx.github.io/2017/06/call-sahith-blog-week-1/)). I am being mentored throughout this process by [James Salsman](http://talknicer.com/about/) who has been associated with the CMUSphinx project for many years.

# Project Overview
The above projects are based on the pronunciation evaluation system described in [Ronanki, Salsman and Bo (2012)](http://www.aclweb.org/anthology/W12-5808). They involve crowdsourcing of a number of audio recordings based on a given set of prompts. These recordings are then presented to transcriptionists who transcribe these recordings. This transcript data is then correlated with the original prompt the recording was based on to obtain intelligibility data. 

One of the overall goals is to design an automated pronounciation evaluation system which can help second language learners help improve their speaking skills to achieve native proficiency. 

My work is to design the data collection platform which does the following:
- Provides a prompt to specific individuals called _voicers_ who read out the prompt and upload the recording to the server.
- Presents _recordings_ collected above to _transcriptionists_ whose task is to transcribe the audio into text.
- Perform analysis with reference to:
	- Quantity of collected data
	- Quality of collected data
	- Quantity of transcriptionists
	- Quality of transcriptionists

To ensure that the data collection process is systematic, we need to maintain a record of transcriptionists and voicers by means of a user management system. Futhermore, the sourcing of the recordings and transcripts can be done by registered users on the system that we have developed as well as from Amazon Mechanical Turk workers by means of external questions.

The system is a RESTful Flask web application which will be hosted on PythonAnywhere/Wikimedia Tool Labs. The data collected will be used by Brij and Sahith  for building the pronounciation evaluation and intelligibility remediation system. The methodologies used for evaluation and validation will be described more in detail in future tasks.

So that's a brief overview of the more immediate tasks. I'll share more later in future posts. So for now, here's to a very productive Summer of Code!