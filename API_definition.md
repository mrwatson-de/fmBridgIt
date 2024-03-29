[![fmBridgIt logo][fmBridgIt logo]][fmBridgIt repo]

# fmBridgIt API definition
[The beginnings of an API between FileMaker 19 and WebViewers]

This document will define the fmBridgIt API between FileMaker 19 and a WebViewer.

Document status: draft / proposal

## Aims & Objectives

(draft)

- make the new web integration functionality in fm 19 as 'FileMakery' as possible, that is:
  - make calling a JavaScript function as easy as calling a script
  - make calling a FileMaker script as easy as calling a JavaScript function
- create a single module to implement this, comprising 
  1. a FileMaker module, fmBridgIt and
  2. a JavaScript module/object, fmBridgIt.js / fmBridgit
- define a simple, unambiguous, future-proof and extensible API

The ultimate aim is:
- to create a de-facto standard for FileMaker developers, so that
- FileMaker developers develop mutually compatible code, making it possible for them
- to share and exchange code (both JavaScript and FileMaker) easily

## Conventions

(draft)

- FileMaker Script names 
  - shall all start with 'fmBridgIt' or '_fmBridgIt' (in order to prevent clashes with other scripts)
  - shall NOT list all script parameters + returns // (discuss)
  - Scripts shall be structured after the rules of FileMaker modules [link?]
  - Scripts shall be seperated into public and private folders
    - Only public scripts may be called from FileMaker
    - Public script names must be stable ay be called from FileMaker
    - Private scripts are internal to the module
- JSON parameters
  - All JSON parameters will use snake_case (which is *far* more consistent than camelCase! - i.e. 'FileMakery')
  - where possible parameter names should be chosen under consideration of the following two aims, whereby the :
    1. clarity of name // It should be cler what is to be passed
    2. readability under the forced a-z ordering of the JSON-parameters in FileMaker // 

- FileMaker Variables
  - Shall be named and defined to leverage the MBS Variable Checking quality control
    - Variable names must comprise of only letters, numbers and "_". No spaces or punctuation.
    - All variables shall be defined
    - MBS Variable Checking should be used

- Script Documentation

@ToDo

## Nomenclature

I would like to introduce the actors of our story:

    Flo' - (Flow[/Florian]) refers to the flow of a FileMaker script
    Widget - refers to the WebViewer
    BridgIt - refers to fmBridgIt, ... but because BridgIt has a split personality
    BridgIt.fm - refers to the FileMaker side of fmBridgIt
    BridgIt.js - refers to the Webviewer side of fmBridgIt

These guys will help to understand and visualize the processes we find  here

For example, a typical conversation, "What is the time in Berlin at the moment?", may look like this:

    User to Flo': "Say, Flo', what is the time in Berlin at the moment?"
    Flo' to BridgIt: "Say, BridgIt, what is the time in Berlin at the moment?"
    BridgIt to Widget: "Say, Widget, what is the time in Berlin at the moment?"
    Widget to moment.js: "Hey, moment.js, what is the time in Berlin at the moment?"
    moment.js to Widget: "It's 'June 4th 2020, 5:29:14 pm'"
    Widget to BridgIt: "It's 'June 4th 2020, 5:29:14 pm'"
    BridgIt to Flo': "It's 'June 4th 2020, 5:29:14 pm'"
    Flo' to User: "It's 'June 4th 2020, 5:29:14 pm'"
    User thinks "Thanks Flo', then I need to take the Bluepill at dotfmp immediately!"

![act_what_is_the_time_in_berlin_at_the_moment](mermaid/act_what_is_the_time_in_berlin_at_the_moment.svg)

Under the surface BridgIt's split personality - which only she knows about - will be doing something like this

    User to Flo': "Say, Flo', what is the time in Berlin at the moment?"
    Flo' to BridgIt: "Say, BridgIt, what is the time in Berlin at the moment?"
    --
    BridgIt.fm hears Flo'
    BridgIt.fm logs this under question #1234
    BridgIt.fm to BridgIt.js: "Say, BridgIt.js, can you ask Widget, what the time is in Berlin at the moment - then call me back with the answer to question #1234"
    (BridgIt.fm waits for a call regarding question #1234)
    BridgIt.js turns to Widget…
    --
    BridgIt to Widget: "Say, Widget, what is the time in Berlin at the moment?"
    Widget to moment.js: "Hey, moment.js, what is the time in Berlin at the moment?"
    moment.js to Widget: "It's 'June 4th 2020, 5:29:14 pm'"
    Widget to BridgIt: "It's 'June 4th 2020, 5:29:14 pm'"
    --
    BridgIt.js hears Widget…
    BridgIt.js calls BridgIt.fm and says the answer to question #1234 is "It's 'June 4th 2020, 5:29:14 pm'"
    BridgIt.fm checks she has received the answer to question #1234 and then proceeds
    BridgIt.fm turns to Flo'
    --
    BridgIt to Flo': "It's 'June 4th 2020, 5:29:14 pm'"
    Flo' to User: "It's 'June 4th 2020, 5:29:14 pm'"
    User thinks "Thanks Flo', then I need to take the Bluepill at dotfmp immediately!"

![act_what_is_the_time_in_berlin_at_the_moment_detailed](mermaid/act_what_is_the_time_in_berlin_at_the_moment_detailed.svg)

Note that:

- Flo' only sees BridgIt (and doesn't really know she has a split personality)
- When he talks to BridgIt he is actually talking to BridgIt.fm
- Similarly Widget only talks to BridgIt.js
- In general Flo' and Widget are morning grumps and tend to throw a tantrum if they speak to each other directly before they've had their morning coffee
- That's why they speak to each other via BridgIt who ensures everybody has had their morning coffee first
- During the day Flo' and Widget can speak to each other directly, but their relationship is so cool they never get an answer. So long as they only want to shoot off at each other and are sure that they've had their morning coffee - that's fine.


## Use Cases

(draft)

### Use Case - From FileMaker call a JavaScript function asynchronously 
### Use Case - From FileMaker call a JavaScript function asynchronously, continuing execution in a script defined in the WebViewer, passing the result forward as a parameter
### Use Case - From FileMaker call a JavaScript function asynchronously, passing a single callback script
### Use Case - From FileMaker call a JavaScript function asynchronously, passing two callback scripts for success and failure

### Use Case - From FileMaker call a JavaScript function synchronously and receive a result back
### Use Case - From FileMaker call a JavaScript function synchronously and receive a result back within a certain timeout

### Use Case - From WebViewer call a FileMaker script asynchronously 
### Use Case - From WebViewer call a FileMaker script asynchronously, continuing execution in a function defined in the FileMaker Script, passing the result forward as a parameter
### Use Case - From WebViewer call a FileMaker script asynchronously, passing a single callback script
### Use Case - From WebViewer call a FileMaker script asynchronously, passing two callback scripts for success and failure

Need an async wrapper/app:
### Use Case - From WebViewer call a FileMaker script synchronously and receive a result back
### Use Case - From WebViewer call a FileMaker script synchronously and receive a result back within a certain timeout


### Use Case - From WebViewer call a FileMaker script to run on server asynchronously 
This would make it possible to pass data back to FileMaker without 'bothering' the current user layout context.

### Use Case - From WebViewer call a FileMaker script to run on server synchronously and receive a result back within a certain timeout 
This may be useful where the webviewer needs large/heavy processing or requests.


---
## Test Cases

(draft)

This bit is still confused and the style needs to be decided

### Test Case "Hello JavaScript Button (FM->WebV)"

From a button in the FileMaker layout pass a message to the web viewer and display in web viewer.

### Test Case "Hello FileMaker Button (WebV->FM)"

From a button in the WebViewer call a FileMaker Script and display in FileMaker.

---

### test Case "Synchronous JavaScript call with parameter and result (FM->WebV->FM)"

The user-developer wishes to call a function in a web-viewer to process the parameter and return the result *without* breaking the script flow.

Example case "increment"


### Test Case "Synchronous FileMaker Script Button (WebV->FM-WebV)"

From a button in the WebViewer call a FileMaker Script and display in FileMaker.

---

### Test Case "WebViewer is ready event"

Disable a WebV-Action Button in FileMaker until the target function is available"

Since it may be bad UX to offer the user buttons in FileMaker to press, which block until the web viewer is ready to process them, it may be desirable 

While a webviewer is loading or 
From a button in the FileMaker layout pass a message to the web viewer and display in web viewer.




@ToDo

## API Methods

@ToDo


[fmBridgIt repo]:https://github.com/mrwatson-de/fmBridgIt
[fmBridgIt logo]:fmBridgIt_logo.png
