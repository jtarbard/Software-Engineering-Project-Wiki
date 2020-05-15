# To Markers (Mark and Amy, or perhaps some postgraduate student)
**Please navigate to the [for markers](#for-markers) and [meetings](#meetings) section. You will find what you need there.**

Before you do any work, run the automatic git cleaning script!\
For Linux, you can use `bash git-clean.sh`.\
For Windows, do the following:
```
git pull --all
git fetch --all
git fetch -p
git branch --merged master | grep -v master | grep -v stable | xargs git branch
```

# Relevant wiki pages for team members
### Coding
[Coding Standard](/Documentation/Coding-Standard)

### Git
[Git Branching Structure](/Documentation/Git-Branching-Structure)\
[Git Commands](/Tutorial/Git-Commands)

### Content in Pages
[Activity Categories](/Research/Activity-Categories)

# Complete Wiki Content Tree
GitLab's wiki is being weird and removed the "More Pages" button. All the wiki pages can still be found via the search bar by typing in `.md`, or just use this [link](https://gitlab.com/search?utf8=%E2%9C%93&snippets=&scope=wiki_blobs&repository_ref=master&search=.md&project_id=16767116)

## Documentation
[Architecture Design](/Documentation/Architecture-Design)\
[Coding Standard](/Documentation/Coding Standard)\
[Demo Mode](/Documentation/Demo-Mode)\
[Git Branching Structure](/Documentation/Git Branching Structure)\
[Testing](/Documentation/Testing)\
[Vertex Information Base](/Documentation/Vertex-Information-Base)\
[[TMP] Common issues & fixes](/Documentation/[TMP] Common issues & fixes)\
[“The Vertex" Design](/Documentation/"The Vertex" Design) **<< bugged link. how to insert quotes?**

### UI-Design
#### 1-Low-Fidelity
[Wireframe Prototypes](/Documentation/UI-Design/1-Low-Fidelity/Wireframe Prototypes)

#### 2-High-Fidelity
[Artboard](/Documentation/UI-Design/2-High-Fidelity/Artboard)

## For Markers
[Commit Credit](/For-Markers/Commit Credit)\
[Project Process Reflection](/For-Markers/Project-Process-Reflection)

## Meetings
[Attendence Record](/Meetings/Attendence Record)\
[Team Meeting 01](/Meetings/Team Meeting 01)\
[Team Meeting 02.1](/Meetings/Team Meeting 02.1)\
[Team Meeting 02.2](/Meetings/Team Meeting 02.2)\
[Team Meeting 03 End of Sprint 1](/Meetings/Team Meeting 03 End of Sprint 1)\
[Team Meeting 04](/Meetings/Team Meeting 04)\
[Team Meeting 05 End of Sprint 2](/Meetings/Team Meeting 05 End of Sprint 2)\
[Team Meeting 06](/Meetings/Team Meeting 06)

## Research
[Activity Categories](/Research/Activity-Categories)\
[Data Gathering with SQIRO](/Research/Data-Gathering-with-SQIRO)\
[Gym Websites Analysis](/Research/Gym-Websites-Analysis)\
[Inspiration Boards](/Research/Inspiration Boards)\
[Research on User Interface](/Research/Research-on-User-Interface)

## Tutorial
[Flask Summary](/Tutorial/Flask-Summary)\
[Git Commands](/Tutorial/Git-Commands)

## External documentation during development
[General Management - Link to Google Spreadsheet](https://drive.google.com/open?id=1k-ubHstqQHhVJ7CCC1BqzZZpsBI-YF3zz7E-1m4k5d0)\
[UI Research - Link to Google Doc](https://drive.google.com/open?id=1dFHQ44MgV2HX5YGJOGtv00Ihh7cH_C_vOREMbwLKXu8)