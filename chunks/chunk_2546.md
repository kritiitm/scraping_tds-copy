### Post 227
**Post URL**: /t/project-2-tds-solver-discussion-thread/169029/227
- **ID**: 613777
- **Author**: Shivaditya Bhattacharya (22f3000819)
- **Created At**: 2025-03-31T07:23:38.044Z
- **Content**:  
  <a class="mention" href="/u/saransh_saini">@Saransh_Saini</a> <a class="mention" href="/u/jivraj">@Jivraj</a> <a class="mention" href="/u/carlton">@carlton</a>
What is the request timeout for each question, especially for the question on YouTube video transcription? I request the timeout to be at least 40-60 seconds as yt-dlp and faster-whisper take take to download the audio, load the model and run it on cpu and get the transcription.<br>
For 259.7 to 351.8 seconds, it is taking around 1.5 mins, but it is giving the correct answer.
So I request you to shorten the length of the audio or increase the request timeout or both in moderation.
Question —&gt; the “question” sent to the api will have the youtube video link, right? Or since the video is same for everyone, can I just have the audio file ready in the project? Will the api be tested against any YouTube video other than the Mystery Story Audiobook link given in the GA question?
Edit: Even with a preprocessed audio file (mp3, speech optimized, 32K), what’s taking the longest time is joining the transcribed sentences into a single string. That alone is taking &gt;50 seconds. Please suggest a way to make it faster.
Regards,<br>
Shivaditya
- **Reactions**: None
- **Post Number**: 227

