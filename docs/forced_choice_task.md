# Forced Choice Task

The Forced Choice task presents a sound file, followed by two buttons. The participant must select one of the buttons before advancing to the next trial.

## Quick Start
- Clone or download a ZIP of the [respository](https://github.com/chunlchan/jsp-template).

![Github download button](./media/forced_choice/github_download.png ':class=elevated-img :size=300')

- Ensure that the "audio" folder and forced_choice.html file are in the same directory.

![Github download button](./media/forced_choice/audio_folder.png ':class=elevated-img :size=300')

- Open the forced_choice.html file in your browser. The web experiment will start automatically.

## Anatomy of a jsPsych file
- Visit the jsPsych anotamy [description here](flanker_task?id=anatomy-of-a-jspsych-file).

## Modifying the Forced Choice Task

To add more trials, locate the *trials* array and append additional lines to the end. Any new audio files referenced in the array should also added to the "audio" folder. Both wav and mp3 sound files are supported.

```js
const trials = [
    {stimulus: "N1-44100.mp3", correct_response:"YES"},
    {stimulus: "N2-44100.mp3", correct_response:"YES"},
    {stimulus: "N3-44100.wav", correct_response:"NO"}, //don't forget to add commas between lines

    //add new lines here
    {stimulus: "mynewsound.wav", correct_response:"YES"},
    {stimulus: "anothersound.wav", correct_response:"YES"}
];
```

Each line in the *trials* array describes an individual trial where *stimulus* refers to the sound file that will be presented to the participant and *correct_response* is the expected correct response from the participant.

```js
{stimulus:"your_sound_file.wav", correct_response:"YES"}
```

## Prolific Integration
- Set up your study on Prolific and obtain the completion URL.
- Insert the completion URL in the *end_experiment* object.

```js
const end_experiment = {
    type: jsPsychHtmlKeyboardResponse,
    stimulus: `
        <h2>Experiment Complete</h2>
        <a href="https://YOUR_COMPLETION_URL_HERE">
        Click here to submit & return to Prolific
        </a>
    `,
    choices: "NO_KEYS",	
}
```
- Clicking on the link at the end of the experiment will direct participants back to the Prolific completion URL.

## Firebase Integration
