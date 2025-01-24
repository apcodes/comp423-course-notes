# Setting up a dev container for Go

* Primary author: [Anish Parepalli](https://github.com/apcodes)
* Reviewer: [Matthew Thornton](https://github.com/mthornton1133)

## Prerequisites
Before we dive in, make sure you have:

1. A GitHub account: If you don’t have one yet, sign up at [GitHub](https://github.com/).
2. Git installed: Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don’t already have it.
3. Visual Studio Code (VS Code): Download and install it from [here](https://code.visualstudio.com/).
4. Docker installed: We need this to run the Dev Container. If you don't have it, [Get Docker here](https://www.docker.com/products/docker-desktop).
5. Command-line basics: Know some basic CLI.  If in doubt, review the Learn a CLI text!


## Creating the Repository
**Local Directory and Git Initialization**  

1. Open Terminal/Command Prompt  
2. Create a new directory for the project
```
mkdir go-project
cd go-project
```
3. Initialize a new Git Repository 
```
git init
```
!!! note "What is the effect of running the ```init``` subcommand?"
    Initialize a folder as a new, empty git repository. 

4. Create a README file 
```
echo "# Go Project" > README.md
echo "Tutorial Link --> [Here](https://apcodes.github.io/comp423-course-notes/)" >> README.md
git add README.md
git commit -m "Initial commit with README"
``` 
### Step 2. Create a Remote Repository on GitHub
1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page
2. Fill in the details as follows:   
```
   Repo Name: Go Project   
   Description: "Making an Hello World in Go!"  
   Visibility: Public 
```
3. Do not initialize the repo with a README, .gitingore, or license. 
4. Click **Create Repository**. 

### Step 3. Link your Local Repository to Github
1. Add GitHub Repository as remote.
```
git remote add origin https://github.com/<your-username>/comp423-course-notes.git
```
Replace <your-username> with your GitHub username. 
2. Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: 
```
git branch -M main. 
```
Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.
3. Push your local commits to the github repo:
```
git push --set-upstream origin main
```  
     
4. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

 
## Setting Up the Development Environment

### Step 1. Add the Development Container Configuration
1. In VS Code open the go-project directory. Go  File > Open Folder.
2. Install Dev Containers extension in VS Code. 
3. Create a .devcontainer directory in the root of your project with the following file inside this “hidden” directory.git    
```
.devcontainer/devcontainer.json
```
4. Place the following code inside your newly created devcontainer.json file:
```
{
    "name": "COMP423 Course Notes",
    "image": "mcr.microsoft.com/vscode/devcontainers/go",
    "customizations": {
        "vscode": {
            "settings": {},
            "extensions": ["golang.go"]
        }
    },
    "postCreateCommand": "go version"
}
```