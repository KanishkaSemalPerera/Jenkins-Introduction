# Jenkins Introduction

A simple, beginner-to-master guide to Jenkins. This README explains everything in easy English, step by step, so anyone — even a total beginner — can understand Jenkins and start using it.

## Table of Contents

1. [What is Jenkins?](#1-what-is-jenkins)
2. [Jenkins vs GitHub Actions](#2-jenkins-vs-github-actions)
3. [Jenkins Controller](#3-jenkins-controller)
4. [Jenkins Agent](#4-jenkins-agent)
5. [Jenkins Job](#5-jenkins-job)
6. [Jenkins Pipeline](#6-jenkins-pipeline)
7. [Getting Started (Step by Step)](#7-getting-started-step-by-step)
8. [Simple Words Glossary](#8-simple-words-glossary)

---

## 1. What is Jenkins?

Jenkins is a **free and open-source tool** that helps developers build, test, and deliver (or deploy) software automatically.

Think of Jenkins like a robot helper. Every time you make a change to your code, Jenkins can automatically:

- Take your new code
- Build it (turn code into a working program)
- Test it (check if it works correctly)
- Deploy it (send it to a server so people can use it)

This whole process is called **CI/CD**:

- **CI (Continuous Integration)** — automatically combining and testing code changes often.
- **CD (Continuous Delivery/Deployment)** — automatically sending the tested code to users or servers.

### Why do people use Jenkins?

- It saves time — no need to build and test manually every time.
- It catches mistakes early — if something breaks, you know right away.
- It works with almost any programming language and tool.
- It has thousands of free plugins to connect with other tools (GitHub, Docker, AWS, Slack, etc).

---

## 2. Jenkins vs GitHub Actions

Both Jenkins and GitHub Actions are tools used for **CI/CD** (automating build, test, and deploy). But they are different in some important ways.

| Feature | Jenkins | GitHub Actions |
|---|---|---|
| **Type** | You install and manage it yourself (self-hosted) | Built directly into GitHub (cloud-hosted) |
| **Setup** | Needs a server and manual setup | Ready to use instantly inside GitHub |
| **Cost** | Free, but you pay for your own server | Free for public repos, limited free minutes for private repos |
| **Where code lives** | Works with any Git tool (GitHub, GitLab, Bitbucket, etc.) | Only works with GitHub |
| **Flexibility** | Very flexible, huge plugin library (2000+ plugins) | Simpler, uses YAML files, fewer plugins but growing |
| **Maintenance** | You must update and maintain the Jenkins server | GitHub maintains everything for you |
| **Best for** | Large companies, complex pipelines, custom needs | Small to medium projects, quick and easy setup |

### Simple Way to Remember

- **Jenkins** = Like owning your own car. More control, but you must maintain it.
- **GitHub Actions** = Like using a taxi. Easy and ready to go, but less control.

---

## 3. Jenkins Controller

The **Jenkins Controller** (previously called "Jenkins Master") is the **brain** of Jenkins.

### What does it do?

- It is the main server where Jenkins is installed.
- It stores all the settings, job configurations, and plugins.
- It shows the web dashboard (the screen you see in your browser).
- It schedules jobs and decides which agent (worker) should run each job.
- It keeps track of build history, logs, and results.

### Simple Explanation

Imagine a manager in an office:

- The manager (Controller) does NOT do the actual work.
- The manager plans the work and tells workers (Agents) what to do.
- The manager keeps records of everything that was done.

⚠️ **Important:** It is not recommended to run heavy build jobs directly on the Controller. The Controller should mainly manage and delegate tasks to Agents.

---

## 4. Jenkins Agent

A **Jenkins Agent** (previously called "Jenkins Slave") is a **worker machine** that actually does the work — building, testing, and running jobs.

### What does it do?

- Receives tasks from the Controller.
- Runs the actual build/test/deploy commands.
- Can be a physical computer, a virtual machine, a Docker container, or a cloud server.
- Sends the results back to the Controller.

### Simple Explanation

Continuing the office example:

- The Agent is the **worker/employee**.
- The manager (Controller) gives instructions.
- The worker (Agent) does the actual job and reports back when finished.

### Why use multiple Agents?

- You can run many jobs at the same time (in parallel).
- Different Agents can have different tools installed (e.g., one Agent for Java, another for Python).
- It reduces load on the main Controller server.

---

## 5. Jenkins Job

A **Jenkins Job** (also called a "Project") is a **single task** that Jenkins performs.

### What is a Job?

A Job is basically a set of instructions you give Jenkins, such as:

- "Download my code from GitHub"
- "Build the project"
- "Run the tests"
- "Deploy the application"

### Types of Jenkins Jobs

1. **Freestyle Project** — The simplest type. You configure steps using the Jenkins web interface (point and click). Good for beginners.
2. **Pipeline** — You write your build steps in code (a `Jenkinsfile`). More powerful and flexible. (Explained in detail below.)
3. **Multibranch Pipeline** — Automatically creates a pipeline for every branch in your Git repository.
4. **Folder** — Used to organize many jobs into groups.

### Simple Explanation

Think of a Job like a **recipe card**. It tells Jenkins exactly what steps to follow, in what order, to complete a task.

---

## 6. Jenkins Pipeline

A **Jenkins Pipeline** is a way to define your entire build process **as code**, using a file called a `Jenkinsfile`.

### Why use a Pipeline instead of Freestyle Jobs?

- All steps are written in code — easy to read, share, and version-control.
- You can store the `Jenkinsfile` in your Git repository along with your project.
- Supports complex workflows (build → test → deploy → notify).
- Easy to reuse and edit.

### Two Types of Pipeline Syntax

1. **Declarative Pipeline** (recommended for beginners) — simpler, structured, easier to read.
2. **Scripted Pipeline** (advanced) — more flexible, written using Groovy programming language.

### Simple Declarative Pipeline Example

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
```

### Explanation of the Example

- `pipeline { }` — Marks the start of the Pipeline.
- `agent any` — Tells Jenkins to run this on any available Agent.
- `stages { }` — A group of all the steps (stages) in order.
- `stage('Build')` — One step in the process; you can name it anything.
- `steps { }` — The actual commands to run inside that stage.

### Simple Explanation

A Pipeline is like a **flowchart** or a **checklist** written in code:

1. First, build the code.
2. Then, test it.
3. Finally, deploy it.

Each stage runs one after another (or in parallel, if configured), and you can see the whole process visually on the Jenkins dashboard.

---

## 7. Getting Started (Step by Step)

Here is a simple beginner roadmap to learn and use Jenkins from scratch:

### Step 1: Install Jenkins

- Download Jenkins from the official website: https://www.jenkins.io/download/
- Install it on your computer or server (Windows, Linux, macOS, or Docker).
- Start Jenkins and open it in your browser (usually `http://localhost:8080`).

### Step 2: Unlock Jenkins

- The first time you open Jenkins, it asks for an unlock code.
- Find the code in the Jenkins installation folder (in a file called `initialAdminPassword`).

### Step 3: Install Suggested Plugins

- Jenkins will ask if you want to install plugins.
- Choose "Install Suggested Plugins" for a good starting setup.

### Step 4: Create an Admin User

- Set up your username and password to log in to Jenkins.

### Step 5: Create Your First Job

- Click "New Item" on the dashboard.
- Choose "Freestyle project" (for beginners) or "Pipeline" (for more control).
- Give it a name and click OK.

### Step 6: Configure the Job

- Add the source code location (e.g., your GitHub repository URL).
- Add build steps (e.g., run a shell command or script).
- Click "Save".

### Step 7: Run the Job

- Click "Build Now".
- Watch the build progress and check the console output for results.

### Step 8: Try a Pipeline

- Create a new "Pipeline" job.
- Write a simple `Jenkinsfile` (see the example above).
- Run it and watch the stages appear on the dashboard.

### Step 9: Add an Agent (Optional, for scaling)

- Go to "Manage Jenkins" → "Manage Nodes and Clouds".
- Add a new Agent (a separate machine or container) to run jobs.

### Step 10: Keep Learning

- Explore plugins (Git, Docker, Slack notifications, etc).
- Learn Declarative Pipeline syntax in more depth.
- Practice building real projects with automated tests and deployment.

---

## 8. Simple Words Glossary

| Term | Simple Meaning |
|---|---|
| **CI/CD** | Automatically building, testing, and delivering code |
| **Controller** | The main Jenkins server that manages everything |
| **Agent** | A worker machine that runs the actual jobs |
| **Job** | A single automated task in Jenkins |
| **Pipeline** | A series of steps (stages) written as code |
| **Jenkinsfile** | A text file containing your Pipeline code |
| **Build** | The process of turning source code into a working program |
| **Plugin** | An add-on that gives Jenkins extra features |
| **Stage** | One step/section inside a Pipeline (e.g., Build, Test, Deploy) |
| **Dashboard** | The web page where you see and manage all your Jenkins jobs |

---

## Summary

- **Jenkins** = an automation tool for building, testing, and deploying software.
- **Jenkins vs GitHub Actions** = Jenkins is self-hosted and flexible; GitHub Actions is built-in and easy.
- **Controller** = the brain/manager that plans and tracks jobs.
- **Agent** = the worker that actually runs the jobs.
- **Job** = a single task Jenkins performs.
- **Pipeline** = a full automated workflow written as code, made of stages.

With these basics, you now have a clear beginner-to-master path to understand and start using Jenkins confidently.
