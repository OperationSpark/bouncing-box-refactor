**Table of Contents**
- [Refactoring Principles](#refactoring-principles)
  - [Separation of Concerns Example](#separation-of-concerns-example)
- [TODOs](#todos)
  - [TODO 1) Create your file structure](#todo-1-create-your-file-structure)
  - [TODO 2) Refactor the file structure](#todo-2-refactor-the-file-structure)
  - [TODO 3) Reflection](#todo-3-reflection)
  - [TODO 4) Refactor index.js comment headers](#todo-4-refactor-indexjs-comment-headers)
  - [TODO 5) Refactor update for separation of concerns](#todo-5-refactor-update-for-separation-of-concerns)
  - [TODO 6) Refactor handleBoxClick for separation of concerns](#todo-6-refactor-handleboxclick-for-separation-of-concerns)
  - [TODO 7) Reflection](#todo-7-reflection)


# Refactoring Principles

This project will focus on "refactoring" an old project: Bouncing Box.

> Refactoring is the process of internally restructuring existing code without changing its external behavior

This project will focus on refactoring for Separation of Concerns.

### Separation of Concerns Example

The main principle of separation of concerns is

> Every file/module/function should perform one task and one task only.

Often, files/functions/modules serve to execute multiple sub-tasks. Consider the following function:

```js
// core logic
function greet() {
  var name = prompt("what is your name?");
  console.log("hello " + name);
  console.log("goodbye " + name);
} 
```

Notice how the `greet` function has 3 distinct sub-tasks that it performs: 
1. asking for a name
2. saying hello with the name
3. saying goodbye with the name

To achieve separation of concerns with this `greet` function, the _implementation_ for each sub-task (the code for _how_ to actually perform a task) should be isolated from one another in the form of _helper functions_

Below is an example of how it may be refactored:

```js
// core logic
function greet() {
  // ask for name
  var name = getStrangersName();

  // say hello
  sayHello(name);  
  
  // say goodbye
  sayGoodbye(name);
}

// helper functions
function getStrangersName() {
  return prompt("what is your name?");
}

function sayHello(name) {
  console.log("hello " + name);
}

function sayGoodbye(name) {
  console.log("goodbye " + name);
}
```

Notice now that the `greet` function simply invokes/calls the other three functions. The main purpose of `greet` is to lay out the high-level logic of the program while the helper functions implement their one task.

In addition, comments have been added to clarify the purpose of each subtask and to organize the `core logic` from the `helper functions`.

Separation of concerns is a principle to program by, not a rule that must be followed. For a program this small, this solution may seem like overkill. However, as our programs grow, organizing code into `core logic` and `helper functions` will keep the logic flowing smoothly, improve the the readability of the program, and simplify the debugging process.

# TODOs

### _Remember to use `control+c` and `control+v` to copy and paste_

## TODO 1) Create your file structure

#### Step 1: Create your folder / files

Right click on the main folder in your workspace and create a new folder with the name: `bouncing-box-refactor`

<img src="https://github.com/OperationSpark/bouncing-box-refactor/blob/master/img/new-folder.png?raw=true" height="250">

Right click on this new folder and create 3 files in that folder: `index.html`, `index.css`, `index.js`

<img src="https://github.com/OperationSpark/bouncing-box-refactor/blob/master/img/new-file.png?raw=true" height="250">

At this point your file structure should look like this:

![alt text](https://github.com/OperationSpark/bouncing-box-refactor/blob/master/img/file-structure.png?raw=true)

#### Step 2: Copy code from `refactor-me.html` into `index.html`

**NOTE: DO NOT USE YOUR OLD BOUNCING-BOX PROJECT**

Open up the file `refactor-me.html` linked at the top of the repository. It contains a solution for bouncing box. Copy the contents of that file into your newly created `index.html` file.

## TODO 2) Refactor the file structure

#### Step 1: move the CSS:

Copy and paste the CSS within the `<style>` tags from `index.html` to `index.css`

Hint: the code you are copy-pasting should look like the code below:

```css
.box {
  /* css for the box... */
}
```

#### Step 2: move the JavaScript

Copy and paste the JavaScript within the `<script>` tags from `index.html` to `index.js`

Hint: the code you are copy-pasting should look like the code below:

```js
/* global $ */
'use strict'
$(document).ready(function(){
  // bouncing box code...             
});
```

#### Step 3: Link `index.js` and `index.css` to `index.html`

At this point, your code should be separated into 3 files. If you were to run your program (in cloud9, right-click on `index.html` and select **Preview**), you would notice that it doesn't work! 

That's because `index.html` is only running the code that it has in its own file. We need to tell it to load in the code written in `index.js` and `index.css`. There are 2 tags that can do this for us: `<link>` and `<script>`

Use your google search powers to look up the following (Hint: include "w3schools" in your search query):
1. `HTML <link> tag`
2. `HTML <script> src attribute`

## TODO 3) Reflection:
Create a new file called `reflections.txt`. Inside, answer the following questions:
- How is the jQuery file being loaded into this project: direct download or Content Delivery Network (CDN)?
- If you load the `index.js` file before the jquery file our program doesn't work. Why? Open the preview in a new tab and look at the console to help you find out why.

## TODO 4) Refactor `index.js` comment headers

Comment headers are incredibly userful for organizing the various components of our program. 

For this project we want the overall structure of `index.js` to look like this:

```js
$(document).ready(function() {

  /////////////////////////////////////////////////
  ////////////// INITIALIZATION ///////////////////
  /////////////////////////////////////////////////

  /* variables and other one-time set up code for the program */

  /////////////////////////////////////////////////
  //////////////// CORE LOGIC /////////////////////
  /////////////////////////////////////////////////

  /* main logic of the program: the update / handleBoxClick functions */

  /////////////////////////////////////////////////
  ////////////// HELPER FUNCTIONS /////////////////
  /////////////////////////////////////////////////

  /* functions for executing sub-tasks of the core logic */

});
```

#### Step 1: Rename the first comment header: `"Initialization"`
#### Step 2: Rename the second comment header: `"Core Logic"`
#### Step 3: Copy the comment header and add a third comment header at the bottom: `"Helper Functions"`
#### Step 4: Move any code that is not below the correct header (hint: variable declarations should all be in `"Initialization"`)

## TODO 5) Refactor `update` for separation of concerns

In this step we will create our first helper functions for the function `update`. Each helper function will implement a sub-task that the `update` function will call in sequence. 

Look at the top of this document for an example of the process outlined below.

_NOTE: All new functions should be declared in the `Helper Functions` section_

#### Step 1: Identify the main sub-tasks that the `update` function performs.

#### Step 2: For each sub-task:
  1. declare a new function in the `"Helper Functions"` section with a name that describes the sub-task. Note: it is likely that it may not need any parameters
  2. identify all code for performing the sub-task and copy-paste it into the new helper function
  3. replace the old code with a call to your new helper function
  
#### Challenge: Can any repeated code be made more abstract/modular?

## TODO 6) Refactor `handleBoxClick` for separation of concerns

Follow the steps outlined above in TODO 5 for `handleBoxClick`

## TODO 7) Reflection:
Inside the `reflections.txt` file answer the following questions:
- In your opinion, what are the pros of refactoring your HTML, CSS, and JavaScript into separate files? What are the cons?
- In your opinion, what are the pros of refactoring your JavaScript code into separate functions? What are the cons?


