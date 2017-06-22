---
title: Transcriber Qualification Architecture
layout: post
---

# Organization
The application is comprised of 4 basic entities
- Users
- Prompts
- Recordings
- Transcripts

The users of the transcriber qualification system are primarily categorized into four groups based on their roles:
- Administrators (Create prompts used for recording tasks, manage other users, collect and manage data)
- Transcribers (Perform transcriptions given recordings)
- Voicers (Record audio for prompts)
- Turkers (A user who accesses the system by means of a HIT)

Voicers, Transcribers and Administrators are the primary categorizations of users. A Turker is a special case of a voicer or transcriber who accesses the system through [Amazon Mechanical Turk](https://www.mturk.com/mturk/welcome). Amazon Mechanical Turk provides us with a wider audience of users who attempt these tasks for rewards. An important benefit it offers is that it allows us to control for specific parameters, such as users from a particular geographical region or separate tasks for different groups. This distinction should enable us to assign rewards to Turkers who complete the basic requirements for the tasks.

Prompts are made use of in the recording task for the speakers to read out. They can be simple words or could be longer phrases. Voicers submit their recordings in the form of MP3 or WAV files through a form. 

The recordings collected from the previous task are then carried forward into the transcription task where registered transcribers can attempt to transcribe the recordings which are presented to them. The task involves a random recording for a specific prompt being played to the user. The transcriber then submits the transcription by means of a simple form input.

The data is continuously presented to the user until all prompts and recordings are exhausted. After this point, the user need not do anything until he is notified of more tasks to perform. As for Turkers, a separate transcription and recording process will be maintained since we are required to maintain a non-varying prompt and recording set for ensuring that the rewards are consistently provided to everyone who attempts the task. This will be handled through a separate HIT process in our Flask application.

So, the architecture of the application is quite straightforward and simple. The data collected from this system will play a more important role in the upcoming weeks. I'll be reporting my application design progress and the data collection results in next week's post. So until then, stay tuned for more! 
