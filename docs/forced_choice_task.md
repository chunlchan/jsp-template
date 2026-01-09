# Forced Choice Task

The Forced Choice task presents a sound file, followed by two buttons. The participant must select one of the buttons before advancing to the next trial.

This template pulls stimuli from external text files, allowing you to create different conditions that can be set through via the `list` URL parameter. Combined with the Taskflow feature in Prolific, it is possible to recruit and distribute participants evenly across the various multiple conditions of your study design.

## Quick Start
- Clone or download a ZIP of the [respository](https://github.com/chunlchan/jsp-template).

![Github download button](./media/forced_choice/github_download.png ':class=elevated-img :size=300')

- Ensure that the "audio" folder, "lists" folder and forced_choice.html file are in the same directory.

![Github download button](./media/forced_choice/audio_lists_folder.png ':class=elevated-img :size=300')


- The lists folder contains two files, list1.txt and list2.txt.
- Each file represents a set of possible stimuli to be presented to participant and should contain a tab separated table with the headers "stimuli" and "correct_response"

| stimuli | correct_response |
| -- | -- |
| N1-44100.mp3 | YES |
| N2-44100.mp3 | NO |
...

From a terminal or shell window, "cd" (which stands for change directory) to the root path of your project

```bash
cd /path/to/your/local/project/
```
?> Tip: You can drag and drop folders into your terminal window

![GIF showing drag-and-drop action](media/firebase/drag_drop.gif ':class=elevated-img :size=620')

- Next, in the terminal or command prompt enter the following Python command:

```python
python -m http.server
```

?> Visit https://www.python.org/downloads/ to download and install Python on your system.

?> In some cases you may need to replace `python` with `python3`.

- Launch a browser and visit http://localhost:8000/forced_choice.html?pid=test&list=list1.txt

![Participant ID url parameter](./media/forced_choice/pid_list_url_param.png ':class=elevated-img :size=600')

?> This passes a participant ID of "test" to the web experiment and will present the stimuli listed in the "list1.txt" file.


## Anatomy of a jsPsych file
- Visit the jsPsych anotamy [description here](flanker_task?id=anatomy-of-a-jspsych-file).

## Modifying the Forced Choice Task

To add more trials to an existing list, simply edit the apprpriate text file (e.g. list1.txt) and add more lines to the existing tab-separated table structure.

To add more lists, duplicate the public/list2.txt and rename to list3.txt. Replace the content of list3.txt with the appropriate stimuli following the same table structure.

As a reminder, any additional lists added are pulled into the web expreiment via the `list` URL parameter.

## Firebase Integration
- Set up your Firebase project following these [instructions](firebase.md) amd take note of your project specific Firebase object.
- In the *forced_choice.html* file, locate the *firebaseConfig* object and replace it with your Firebase project's configuration.

```js
const firebaseConfig = {
    //replce these with your the configuration from your Firebase project 
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

- Your web experiment will now be connected to Firebase and responses from participants will be saved to Firebase's Realtime Database.

## Firebase Secure Rules
- From the Firebase web console, select "Realtime Database" -> "Rules"

![Firebase Realtime Database rules panel](./media/forced_choice/rtdb_rules.png ':class=elevated-img :size=400')

- Replace the current rules with the ones below.

```js
{
    "rules": {
        ".read": false,
        ".write": false,
        "data": {
            "$pid": {
                "$pushKey": {
                    ".read": false,
                    ".write": true,
                    ".validate": "$pid == newData.child('pid').val()"
                }
            }
        }
    }
}
```

## Prolific Integration
- After completing the "Deployment to Firebase Hosting" steps, take note of your Firebase public URL (e.g. https://my-project.web.app).
- Log into your Prolific account and initate a new study.
- "Data Collection" -> "What's the URL of your study", enter your Firebase web app's public URL.

![Prolific URL parameters screenshot](./media/forced_choice/prolific_study_url.png ':class=elevated-img :size=400')

- "Recording Prolific IDs" -> Select "URL Parameters", then click "Edit".

![Prolific URL parameters screenshot](./media/forced_choice/prolific_url_params.png ':class=elevated-img :size=600')

- Under "PROLIFIC PID" enter "pid" (all lowercase). Click "Add Parameters".

![Prolific URL parameters screenshot](./media/forced_choice/prolific_url_params_edit.png ':class=elevated-img :size=400')

- The new set of URL parameters should now look like this:

![Prolific URL parameters screenshot](./media/forced_choice/prolific_url_params_new.png ':class=elevated-img :size=600')



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


## Taskflow Setup on Prolific
Prolific has a new feature called [Taskflow](https://researcher-help.prolific.com/en/articles/445142-taskflow-academic-multiple-conditions) that will evenly distribute participants across multiple URLs in a single study.

- Create a file named *urls.csv*
- Add URLs pointing to the appropriate lists of your study to *urls.csv* (one URL per line). This may look something like the following:
    - https://my-project.web.app/?list=list1.txt
    - https://my-project.web.app/?list=list2.txt
    - https://my-project.web.app/?list=list3.txt
    - etc...

- Log in to Prolific, create a new study or select an existing study.
- Under "How do you want to collect your data?", select "Taskflow"<br/>
![taskflow](./media/forced_choice/taskflow.png ':class=elevated-img :size=300')
- Upload urls.csv to Prolific <br/>
![taskflow section](./media/forced_choice/taskflow_upload1.png  ':class=elevated-img :size=400')
![taskflow upload](./media/forced_choice/taskflow_upload2.png  ':class=elevated-img :size=400')

- Enter the total number of participants and the distribution across each unique URL. <br/>
![task flow distribution](./media/forced_choice/taskflow_distribution.png  ':class=elevated-img :size=500')

- Click "Save as Draft" on the study page to save changes.