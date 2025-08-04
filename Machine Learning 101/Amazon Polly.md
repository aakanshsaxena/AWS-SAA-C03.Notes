> [!note]- AI
> #### Amazon Polly: Overview and Features
> - **Purpose:** Amazon Polly is a Text-to-Speech (TTS) service that converts text into lifelike speech. It is a powerful tool for adding voice capabilities to applications. Polly is a one-to-one service and does not perform language translation.
> - **Speech Synthesis:** Polly offers two main speech synthesis engines:
>     - **Standard TTS:** Uses a concatenative approach, stitching together short speech segments to produce a complete utterance.
>     - **Neural TTS (NTTS):** Uses deep learning to generate more natural, lifelike, and expressive speech that sounds more human.
> - **Audio Output and Formats:** The service outputs speech in various audio formats, such as MP3 and PCM, which you can choose based on your application's integration needs.
> #### Controlling Speech with SSML
> - **Speech Synthesis Markup Language (SSML):** This is an XML-based markup language that you can use to control how Polly synthesizes your text. It allows you to add nuances to the speech, such as adjusting the pronunciation, pitch, volume, and speaking rate. SSML is essential for creating high-quality, natural-sounding audio.
> - **Whispering:** Polly can be directed to speak text in a whispered voice rather than a normal voice. This is done by enclosing the text in a specific SSML tag, like `<amazon:effect name="whispered">`, and is useful for creating more dynamic and context-aware audio.
> - **Newscaster Speaking Style:** A specific speaking style available for a subset of neural voices in Polly. It can be applied to text using an SSML tag, such as `<amazon:domain name="news">`, which makes the speech sound like it is being delivered by a professional news anchor.
> #### Integration and Use Cases
> - **API Integration:** Polly is a backend service. Its primary use is to be integrated into applications via AWS APIs or SDKs, allowing for programmatic text-to-speech conversion.
> - **Platform Integration:** You can integrate Polly with other platforms, such as WordPress, to automatically convert articles into spoken audio using a **WordPress plugin**.
> - **Common Use Cases:** Polly is used for a variety of applications, including creating audio versions of articles, building interactive voice response (IVR) systems, and developing educational content with expressive narration.
> #### Definitions
> - **Speech Synthesis Markup Language (SSML):** An XML-based markup language that allows developers to add nuances and control the attributes of synthesized speech, such as pronunciation, pacing, pitch, and tone, to make the output sound more natural and expressive.
> - **Whispering in Speech Synthesis:** An effect that can be applied to text using SSML to cause the text to be spoken in a hushed or soft tone, rather than in the normal speaking style of the voice.
> - **Newscaster Speaking Style:** A speaking style available in Amazon Polly for certain neural voices. It uses a different rhythm and tone to make the synthesized speech sound like it is being delivered by a news anchor.
> - **WordPress Plugin:** A piece of software that can be installed on a WordPress website to add new features or functionality. Plugins enable users to extend their site's capabilities without writing custom code, such as adding text-to-speech functionality.

- Converts text into "life-like speech"
- Text (language) -> speech (language), no translation
- Standard TTS = Concatenative (phonemes)
- Neural TTS = phonemes -> spectograms -> vocoder -> audio
	- much more human/natural sounding but more complex
- MP3, Ogg Vorbis, PCM
More Info
- Speech synthesis markup language (SSML) gives additional control over how Polly generates speech
	- emphasis
	- pronounciation
	- whispering
	- "Newscaster" speaking style
