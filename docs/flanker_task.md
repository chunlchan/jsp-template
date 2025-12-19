# Flanker Task

The Flanker Task measures attention and cognitive control. Participants respond to a central target such as an arrow while ignoring surrounding distractor stimuli (flankers) that may either match (congruent) or oppose (incongruent) the target. The task tests the ability to focus and suppress interference.

- Congruent trial: The flankers match the target (e.g., "> > > > >" or "< < < < <").
- Incongruent trial: The flankers oppose the target (e.g., "> > < > >" or "< < > < <").


## Quick Start
- Download the [flanker_demo.html file](https://github.com/chunlchan/jsp-template/blob/main/flanker_demo.html) from the repository.
- Open the HTML file in your browser. The web experiment will start automatically.

![Github download button](./media/flanker/github_download.png ':class=elevated-img :size=300')

## Anatomy of a jsPsych file
- To understand how a jsPsych file works, it helps to know where the programming logic is defined. As you'll see, most of the functionality is handled inside the script tags.

```html
<script>... </script>
```

- The major events in the flow of the experiment are defined as *const* variables

```js
const welcome_trial = { ... } //welcome message
const instructions_trial = { ... } //instructions
const flanker_timeline = { ... } //the repetitive element of the study
const end_experiment = { ... } //end-of-experiment message
```

- The *flanker_timeline* variable contains a *timeline_variables* parameter defines the main repeating element of the study. In the case of the Flanker task, these are arrows in various configurations that are displayed to the participant.

```js
const flanker_timeline = {
    ...,
    timeline_variables: [
        //four trials
        {stimulus: "< < < < <", type:"congruent_left", correct_response:"f"},
        {stimulus: "> > > > >", type:"congruent_right", correct_response:"j"},
        {stimulus: "< < > < <", type:"incongruent_left", correct_response:"j"},
        {stimulus: "> > < > >", type:"incongruent_right", correct_response:"f"}  
    ],
    randomize_order: true, //randomizes order of timeline variables
    repetitions: 2 //this will cycle through timeline variables twice for a total of 8 trials
}
```

- The *flanker_timeline* variable also contains a *timeline* parameter which is simply an ordered list of events. For the Flanker task, we want to first display a fixation cross followed by the stimulus arrows.

```js
timeline: [
    //fixation
    { ... },

    //stimulus arrows
    { ... }
]
```


- For the fixation cross, we use the [*jsPsychHtmlKeyboardResponse*](https://www.jspsych.org/latest/plugins/html-keyboard-response/) plugin.

```js
{
    type: jsPsychHtmlKeyboardResponse,
    //stimulus contains HTML wrapped in backticks `...`
    //here we're just displaying the + character in <h1> tags for the largest possible font size
    stimulus: `
        <h1>+</h1>
    `,
    choices: "NO_KEYS",//keyboard presses are ignored
    trial_duration: 500//this trial sits for 500 milliseconds before moving on
},

```

- The actual stimulus arrows are presented to the participant leveraging the same *jsPsychHtmlKeyboardResponse* jsPsych plugin.

```js
{
    type: jsPsychHtmlKeyboardResponse,
    stimulus:function(){
        let html = `
            //stimulus arrows defined in "timeline_variables" are inserted here
            <h1>${jsPsych.evaluateTimelineVariable('stimulus')}</h1>
        `;
        return html;
    },
    choices: ['f', 'j']//participant must press f or j on their keyboard to proceed
}

```

- Finally the individual sections (welcome, instructions, timeline, end_experiment ) are sequenced together in a master timeline and passed to the jsPsych runner.

```js
let master_timeline = []; //first create an empty array

//add welcome trial followed by instrictions, the main experiment timeline and finally the experiment end message. 
master_timeline.push(welcome_trial);
master_timeline.push(instructions_trial);
master_timeline.push(flanker_timeline);
master_timeline.push(end_experiment);

//pass the master timeline to the jsPsych runner
jsPsych.run(master_timeline);
```

## Add Trials
-  To add more trials to the Flanker task, first locate the *timeline_variables* variable.

```js
timeline_variables: [
    {stimulus: "< < < < <", type:"congruent_left", correct_response:"f"},
    {stimulus: "> > > > >", type:"congruent_right", correct_response:"j"},
    {stimulus: "< < > < <", type:"incongruent_left", correct_response:"j"},
    {stimulus: "> > < > >", type:"incongruent_right", correct_response:"f"}  
]
```

- Add additional lines to the timeline_variables array to increase the number of trials.

```js
timeline_variables: [
    {stimulus: "< < < < <", type:"congruent_left", correct_response:"f"},
    {stimulus: "> > > > >", type:"congruent_right", correct_response:"j"},
    {stimulus: "< < > < <", type:"incongruent_left", correct_response:"j"},
    {stimulus: "> > < > >", type:"incongruent_right", correct_response:"f"}, //don't forget to separate each line with a comma
    
    //new lines here
    {stimulus: "< < < < <", type:"congruent_left", correct_response:"f"}//last line does not require a comma
]
```

- Modify the randomization and number of repetitions as needed.

```js
randomize_order: true, //randomizes order of timeline variables
repetitions: 2 //will cycle through timeline variables twice for a total of 8 trials
```
