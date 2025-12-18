
# Firebase Setup

## Create a new Firebase project

<img src="media/firebase/create_firebase_prj.png" alt="Firebase create new project button" style="max-width:400px;"></img>

- Enter a project name
- Unselect the "Join the Google Developer Program" toggle

<img src="media/firebase/prj_name.png" alt="Project name form" style="max-width:400px;"></img>

## Setup Realtime Database

- From the Build section of left navigation menu, select "Realtime Database" -> "Create Database" and select "United States"as the location. 

<img src="media/firebase/rtdb_1.png" alt="Realtime Database create button" style="max-width:600px;"></img>
<img src="media/firebase/rtdb_2.png" alt="Realtime Database location drop down menu" style="max-width:600px;"></img>

- Select "Start in Test Mode" for Security Rules (stronger rules are available in the template folders)

<img src="media/firebase/rtdb_3.png" alt="Realtime Database security rules options" style="max-width:600px;"></img>

## Obtain Firebase Config Object

- Click the gear icon next to "Project Overview" and select "Project Settings".

<img src="media/firebase/gear_icon.png" alt="Gear icon button" style="max-width:400px;"></img>

- Select the web </> icon.

<img src="media/firebase/web_icon.png" alt="Web icon button" style="max-width:400px;"></img>


- Enter a nickname for the web app, then click "Register app".

<img src="media/firebase/register_app.png" alt="Web app registration form" style="max-width:400px;"></img>

You should no see your project specific Firebase config object that will look something like this:

```js
const firebaseConfig = {
  apiKey: "1234ABCD",
  authDomain: "your-project-id.firebaseapp.com",
  databaseURL: "https://your-project-id-default-rtdb.firebaseio.com",
  projectId: "your-project-id",
  storageBucket: "your-project-id.firebasestorage.app",
  messagingSenderId: "1234567",
  appId: "1234ABCD"
};
```
This block of code will need to be added to your web experiment template. Instructions for this are available in the web template specific pages.

## Deployment
Download and install the following:
- [Node and NPM](https://nodejs.org/en)
- [Firebase CLI](https://firebase.google.com/docs/cli/)

From a terminal or shell window, "cd" (which stands for change directory) to the root path of your project

```bash
cd /path/to/your/local/project/
```
?> Tip: You can drag and drop folders into your terminal window

<img src="media/firebase/drag_drop.gif" alt="GIF showing drag-and-drop action" style="max-width:620px"/>

To set up the Firebase deployment pipeline 
```bash
firebase login
```

If prompted with "Allow Firebase to collect CLI and Emulator Suite usage and error reporting information? (Y/n)", enter "N" for no.

This will launch your default browser and prompt you to log in with your Firebase account.

Next, if this is the project's first time interacting with Firebase, you will need to run the following:
```bash
firebase init
```
- Using the arrow keys, scroll down to "Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys" and use the spacebar to select.
- Next, select "Use an existing project".
- Using the arrow keys select your project.
    - 'What do you want to use as your public directory?' prompt, enter a forward slash ('/').
    - 'Configure as a single-page app (rewrite all urls to /index.html)?' prompt, enter 'N'.
    - 'Set up automatic builds and deploys with GitHub?' prompt, enter 'N'
    - 'File //index.html already exists. Overwrite?', enter 'N'

<img src="media/firebase/firebase_hosting_CLI.png" alt="Firebase Hosting Command Line Screenshot" style="max-width:620px"/>


Finally, run the deploy command
```bash
firebase deploy
```
This will upload the html files to firebase and will generate a public URL (e.g. https://my-project.web.app) which can be distributed to online participants.