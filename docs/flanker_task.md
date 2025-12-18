# Flanker Task

The Flanker Task measures attention and cognitive control. Participants respond to a central target such as an arrow while ignoring surrounding distractor stimuli (flankers) that may either match (congruent) or oppose (incongruent) the target. The task tests the ability to focus and suppress interference.

- Congruent trial: The flankers match the target (e.g., "> > > > >" or "< < < < <").
- Incongruent trial: The flankers oppose the target (e.g., "> > < > >" or "< < > < <").


## Demo
Try a working demo of the [Flanker Task here](/flanker_demo.html ':ignore').

## Quick Start
- Download the flanker_demo.html file from the [Github repo](https://github.com/chunlchan/jsp-template/blob/main/flanker_demo.html).
-  Locate the timeline_variables variable:

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

- Modify the randomization and number of repetitions as needed

```js
randomize_order: true, //randomizes order of timeline variables
repetitions: 2 //will cycle through timeline variables twice for a total of 8 trials
```