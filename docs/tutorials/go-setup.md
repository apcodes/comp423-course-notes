# Setting up a Dev Container for Go

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

1. Open Terminal/Command Prompt.  
2. Create a new directory for the project.
```
mkdir go-project
cd go-project
```
3. Initialize a new Git Repository. 
```
git init
```
!!! note "What is the effect of running the ```init``` subcommand?"
    Initialize a folder as a new, empty git repository. 

4. Create a README file. 
```
echo "# Go Project" > README.md
echo "Tutorial Link --> [Here](https://apcodes.github.io/comp423-course-notes/tutorials/go-setup/)" >> README.md
git add README.md
git commit -m "Initial commit with README"
``` 
### Step 2. Create a Remote Repository on GitHub
1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
2. Fill in the details as follows:   
```
   Repo Name: Go Project   
   Description: "Making Hello World in Go!"  
   Visibility: Public 
```
3. Do not initialize the repo with a README, .gitingore, or license. 
4. Click **Create Repository**. 

### Step 3. Link your Local Repository to Github
1. Add GitHub Repository as remote.
```
git remote add origin https://github.com/<your-username>/Go-Project
```
Replace `<your-username>` with your GitHub username. 
2. Check your default branch name with the subcommand `git branch`. If it's not main, rename it to main with the following command: 
```
git branch -M main. 
```
Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.
3. Push your local commits to the github repo:
```
git push --set-upstream origin main
```  
     
4. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use `git log` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

 
## Setting Up the Development Environment

### Step 1. Add the Development Container Configuration
1. In VS Code open the go-project directory. Go  File > Open Folder.
2. Install Dev Containers extension in VS Code. 
3. Create a `.devcontainer` directory in the root of your project with the following file inside this “hidden” directory.git    
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
2. Reopen the project in dev container by pressing ctrl + shift + p (cmd + shift + p for mac) then type "Dev Containers: Reopen in Container".   
3. Using the **go version** command in the terminal, you can see what version of go your on.
```
go version
```

## Creating Your Go Project
1. if your not in your directory already, cd into your go-project directory.
```
cd go-project
```
2. Initialize a Go module
```
go mod init hello-comp423
```
This sets up a new Go project and creates a go.mod file, which helps manage dependencies.
3. Create your main file: Inside your project folder, create a new file named main.go.
```
touch main.go
```
Edit `main.go` to display “Hello COMP423”: Open the file in VSCode and add the following code:
```
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```

### To Run the Program
There are 2 different ways to run the program. The first method is the ```go run``` command.   
This is a simplified way to compile and run the Go program in a single line:
```
go run main.go
```

The second method is to use `go build`.   

Use `go build` to compile the Go program into an executable file.
```
go build
```
This will create an executable file named `hello-comp423` in the same directory. To run it, type:
```
./hello-comp423
```

This is similar to using gcc to compile a C program, which we did in Comp 211, where you would run:

```
gcc main.c -o output
./output
```
In Go, go build handles the compilation step and produces the executable directly.

Congratulations you now have a working Dev Container to create a Go Project in!
Many parts of this tutorial are inspired by Kris Jordan’s [Starting a Static Website Project with MkDocs](https://comp423-25s.github.io/resources/MkDocs/tutorial/#what-is-a-development-dev-container).