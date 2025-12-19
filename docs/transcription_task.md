# Transcription Task

The Transcription Task task presents a sound file, followed by an open ended textbox. The participant must enter some text into the textinput box before proceeding to the next trial.

## Quick Start
- Clone or download a ZIP of the [respository](https://github.com/chunlchan/jsp-template).

![Github download button](./media/forced_choice/github_download.png ':class=elevated-img :size=300')

- Ensure that the "audio" folder and forced_choice.html file are in the same directory.

![Github download button](./media/forced_choice/audio_folder.png ':class=elevated-img :size=300')

- Open the transciption_demo.html file in your browser. The web experiment will start automatically.

## Anatomy of a jsPsych file
- Visit the jsPsych anotamy [description here](flanker_task?id=anatomy-of-a-jspsych-file).

## Modifying the Transcription Task

To add more trials, locate the *trials* array and append additional lines to the end. Any new audio files referenced in the array should also added to the "audio" folder. Both wav and mp3 sound files are supported.

```js
const trials = [
    {stimulus: "N1-44100.mp3", correct_response:"He looked at the sleeves"},
	{stimulus: "N2-44100.mp3", correct_response:"Bob wore a watch on his wrist"},
    {stimulus: "N3-44100.wav", correct_response:"Mom looked at the juice"}, //don't forget to add commas between lines

    //add new lines here
    {stimulus: "mynewsound.wav", correct_response:"The boy kicked the ball"},
    {stimulus: "anothersound.wav", correct_response:"Big dogs can be dangerous"}
];
```

Each line in the *trials* array describes an individual trial where *stimulus* refers to the sound file that will be presented to the participant and *correct_response* is the expected correct transcription.

```js
{stimulus:"wife_husband_001.wav", correct_response:"The wife helped her husband"}
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
- See Firebase Intergration section of the [Forced Choice task documentation](./forced_choice_task.md)

## Firebase Secure Rules
- See Firebase Secure rules section of the [Forced Choice task documentation](./forced_choice_task.md)

## Prolific Integration Secure Rules
- See Prolific Integration rules section of the [Forced Choice task documentation](./forced_choice_task.md)
