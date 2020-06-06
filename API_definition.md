[![fmBridgIt logo][fmBridgIt logo]][fmBridgIt repo]

# fmBridgIt API definition
[The beginnings of an API between FileMaker 19 and WebViewers]

This document defines the fmBridgIt API between FileMaker 19 and a WebViewer.

## Aims & Objectives

(draft)

- make the new web integration functionality in fm 19 as 'FileMakery' as possible, that is:
  - make calling a JavaScript function from FileMaker as easy as calling a script
  - make calling a FileMaker script as easy as calling a JavaScript function
- create a single module to implement this, comprising 
  1. a FileMaker module, and
  2. a JavaScript module/object
- define a simple, unambiguous, future-proof and extensible API

The ultimate aim is:
- to create a de-facto standard for FileMaker developers, so that
- FileMaker developers develop mutually compatible code, making it possible for them
- to share and exchange code (both JavaScript and FileMaker) easily

## Conventions

(draft)

- FileMaker Script names 
  - shall all start with 'fmBridgIt' (in order to prevent clashes with other scripts)
  - shall NOT list all script parameters + returns // (discuss)
  - Scripts shall be structured after the rules of FileMaker modules [link?]
  - Scripts shall be seperated into public and private folders
  
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

## Use Cases

@ToDo

## API Methods

@ToDo


[fmBridgIt repo]:https://github.com/mrwatson-de/fmBridgIt
[fmBridgIt logo]:fmBridgIt_logo.png
