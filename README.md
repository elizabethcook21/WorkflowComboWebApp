# Summary
This is the web application version of the WorkflowCombo command line tool.

# Notes
This app is in the early stages of development. All of the commented-out code in the app is code Dr. Piccolo wrote for his app ToolJig and that I used as reference to learn Vue and Javascript. It can definitely be deleted from this app whenever. When I started developing the app, I used PhpStorm but Dr. Piccolo prefers Visual Studio Code. There is just one file, index.html which is divided into different sections that correspond with a Vue app.

# Next Steps for Web Development
Right now, the app asks the user to upload at least one file. There are two text boxes underneath that upload button (they correspond with data elements text and text1) and those are just used for debugging purposes at the moment. They will be deleted later. 
1. Once a user has uploaded the files and they've been parsed, we need to get the very beginning inputs and the very end outputs and set those as "workflow" inputs and outputs (these don't go in the "steps" section). These are the big picture inputs and outputs.
2. Next, the app should run an algorithm to match inputs and outputs for the steps to see if anything can be processed automatically. In the command line tool, this was very simple. If there was one input and one output with the same data type, go ahead and match them. 
3. Next, generate the questions for the user to answer about what goes where. The command line tool asked 4 different questions about where the input came from (a previous step's output, an output from an entirely different step, a new external source, or an existing external source). 
4. Once the user has answered the questions, generate a workflow (cwl file) for the user to save to their computer.

# Unneccesary, but potentially helpful To-Do's
1. Eventually I'd like to allow the user to drag and drop the files they input to determine the order in which they will be organized in the workflow (rather than renaming the files to start with 01, 02, etc..)
2. I'd like to split this webpage down the middle and have the questions on the left side, and a preview of the workflow they're building on the right side (so they know what it looks like)

*Authors: Elizabeth C. Anderson and Dr. Stephen Piccolo (BYU)*
*May 2020*
