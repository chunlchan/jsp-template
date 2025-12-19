# Background Noise Task

The Background Noise Task plays a continuous sound file (noise, babble etc...) while presenting text prompts to the participant.

## Quick Start
- Clone or download a ZIP of the [respository](https://github.com/chunlchan/jsp-template).

![Github download button](./media/forced_choice/github_download.png ':class=elevated-img :size=300')

- Ensure that the "audio" folder and bgnoise_textprompt.html file are in the same directory.

![Github download button](./media/bg_noise/audio_folder.png ':class=elevated-img :size=300')

- Open the bgnoise_textprompt.html file in your browser. The web experiment will start automatically.

## Anatomy of a jsPsych file
- Visit the jsPsych anotamy [description here](flanker_task?id=anatomy-of-a-jspsych-file).

## Modifying the Background Noise Task

To add more trials, locate the *trials* array and append additional lines to the end. Any new audio files referenced in the array should also added to the "audio" folder. Both wav and mp3 sound files are supported.

```js
//list of prompts to appear on screen
const trials = [
    {textprompt:"Tell us about where you grew up?"},
    {textprompt:"What is your favorite food and why?"}
    //add more prompts here as needed
];
```

