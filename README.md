# Event Registration Form — DevOps Lab

This project follows the Event Registration Application described in the faculty DevOps laboratory notes. It supports Experiment 1 (registration form), Experiment 2 (Git/GitHub), Experiment 3 (modify and push a change), and Experiment 5 (Jenkins pipeline). Experiment 4's standalone Freestyle job commands are included below.

## Project files

- `public/index.html` — registration form
- `public/style.css` — form styling
- `public/script.js` — client-side submission
- `server.js` — Express server, validation, security headers, rate limiting, and text-file storage
- `data/registrations.txt` — starts empty; successful submissions append one JSON record per line
- `Jenkinsfile` — Windows Jenkins pipeline from the faculty notes

## Run Experiment 1 on Windows

1. Install Node.js LTS.
2. Open Command Prompt in this project folder.
3. Run:

   ```bat
   npm install
   npm start
   ```

4. Open `http://localhost:3000` in your browser.
5. Submit a test registration. The page should show `Registration completed successfully.` and the record should be appended to `data/registrations.txt`.
6. Stop the server with `Ctrl+C`.

Use test details only. Do not commit real personal registration data to a public repository.

## Experiment 2 — first GitHub upload

Create an empty GitHub repository named `event-registration` (do not initialize it with a README), then run these commands in this project folder, replacing the URL with your own repository URL:

```bat
git init
git add .
git commit -m "First commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/event-registration.git
git push -u origin main
```

If Git asks for your identity, configure it with your own name and email using `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"`.

## Experiment 3 — modify the heading

In `public/index.html`, change:

```html
<h1>Event Registration Form</h1>
```

to:

```html
<h1>DevOps Event Registration Form</h1>
```

Then run:

```bat
git status
git add .
git commit -m "Update event registration heading"
git push
```

## Experiment 4 — Jenkins Freestyle build command

In Jenkins, create a **Freestyle project** named `DevOps_First_Job`. Under **Build → Add Build Step → Execute Windows batch command**, enter:

```bat
echo ==========================
echo Jenkins Build Started
echo ==========================
echo Welcome to DevOps Lab
echo Build completed successfully
```

Click **Save → Build Now → Build #1 → Console Output**.

## Experiment 5 — Jenkins pipeline

This `Jenkinsfile` uses Windows `bat` steps, so the Jenkins agent must be a Windows agent with Git and Node.js/npm available on its PATH. Ensure the project is pushed to GitHub and `package-lock.json` is committed. Create a Jenkins **Pipeline** item named `Event-Registration-CI-CD`, choose **Pipeline script from SCM**, SCM **Git**, enter your repository URL, branch `*/main`, and script path `Jenkinsfile`. Save and click **Build Now**.

The pipeline runs checkout, `npm ci`, JavaScript syntax checks, and a demonstration deployment stage. The Deploy stage only prints messages; it does not deploy to a live server.

## Validation notes

The source structure and program logic were reconstructed from the supplied faculty notes. Run `npm install` once before your first GitHub upload. This installs the listed packages and generates `package-lock.json`, which must also be committed for the faculty pipeline's `npm ci` command to work. The browser/server workflow and automated pipeline still require the listed software to be installed on the machine/Jenkins agent.
