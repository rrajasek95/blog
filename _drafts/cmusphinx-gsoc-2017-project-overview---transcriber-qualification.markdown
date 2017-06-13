---
title: CMUSphinx GSoC 2017 Project Overview - Transcriber Qualification
layout: post
---

# Background
CMUSphinx is one of the most active open source communities providing state of the art tools for speech recognition. The project's site can be found [here](https://cmusphinx.github.io/) and the Github repository [here](https://github.com/cmusphinx). I got to find out about CMUSphinx when doing research about my final year project on forced transcript alignment. It gave me access to a lot of useful material and some crucial insights about it which helped towards my final project. Finding out that it was one of the Google Summer of Code selected organizations this year was pleasant news to me, hence leading me to apply to it. 

I am working on the project _[Transcriber Qualification](https://summerofcode.withgoogle.com/projects/#6044456057831424)_, whose goal is to act as a support to two other projects -- _[Pronunciation Intelligibility Remediation](https://summerofcode.withgoogle.com/projects/#6205453974372352)_ by Brij (whose blog you can check out [here](https://pronunce.blogspot.in/)) and _[Computer Assisted Learning Including Speaking Skills](https://summerofcode.withgoogle.com/projects/#5526592114655232)_ by Sahith Dambekodi (who posted to the CMUSphinx blog [here](https://cmusphinx.github.io/2017/06/call-sahith-blog-week-1/)).

# Project Overview
The above projects are based on the pronunciation evaluation system designed by [Ronanki et. al.](http://www.aclweb.org/anthology/W12-5808). They involve crowdsourcing of a number of audio recordings based on a given set of prompts. These recordings are then presented to transcriptionists who transcribe these recordings. This transcript data is then correlated with the original prompt the recording was based on to obtain intelligibility data.