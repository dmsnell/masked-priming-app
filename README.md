# Masked Priming Suite

## General overview

The purpose of this app is to produce predefined sequences of text, imagery, or sounds and record how long it takes someone who is using the app to respond to those sequences. These sequences form a chain of stimuli and and target or expected responses. The user's response-times are recorded and may contain additional information such as whether or not the response was correct, how many occurances of the particular sequence it took to obtain a correct result, or other possible addenda.

Each experimental session is described in a plain text file editable in any common text editor such as Notepad or Sublime Text or even the venerable Vim. Additionally, the app provides a visual system for building these configuration files without having to know the details of the format. The sequences in the file may be run sequentially or in a randomized order. Questions may be repeated a certain number of times or when their response is incorrect. Sequences may be skipped when certain conditions are met, such as when related sequences have received accurate responses.

The experimental sessions will either be run individually by the research subjects or in the presence of a test operator who might control the input to the app, such as when a subjective assesment of their response is required or when the required computer skills would negatively impact the results of the study.

## Historic precedents

This app is being designed as a successor to the [DMDX app for measuring reaction times to visual and auditory stimuli](http://www.u.arizona.edu/~kforster/dmdx/dmdx.htm). DMDX was built during a time when the physical hardware was a significant limiting factor in the design. Today, however, the ubiquity of fast computing has made it possible to reproduce the quality and accuracy of the testing suite while using modern higher-level software techniques. This app is designed to maximize two goals:

 - Make it easy for researchers to build experiments
 - Operate universally on multiple platforms

The first goal means that the idioms used to generate the sequence of testing steps should be simple to recognize without having to learn a complicated system. The _item files_ used by DMASTR and DMDX are somewhat arcane albeit powerful in their syntax. A proper redesign might be able to trade some of the terseness of the item file with a verbosity that expresses the intent of each step more clearly. The usefulness of any such redesign would of course have to outweight the familiarity of researchers in the field with the existing synax.

The second goal will inform the choice of language and platform used to design the app. Today, this universality comes unquestionably through the Web using HTML, JavaScript, and CSS. Modern extensions to the JavaScript language, such as the `performance.now()` high-precision timer and the `requestAnimationFrame()` function provide even higher levels of accuracy and control than the former DirectX environment used in DMDX. Further, the JavaScript _EventLoop_ provides an obvious and pain-free way of interacting with user input. Properly designed, this app should run just as seamlessly in a mobile browser as it does in a desktop browser, or even on such platforms as a desktop app via [Electron](http://electron.atom.io).

## Major components

 - [ ] Specification for the domain-specific configuration language
 - [ ] Linter for the configuration file language
 - [ ] Presentation of the configuration files for actually running the experiments
 - [ ] Logging middleware to measure, track, and record responses
 - [ ] Report generator for summarizing and presenting the results of a given experiment or group of experimental trials
 - [ ] Debugging and testing suite to perform meta-analysis on the app itself for validation of its operation and tolerances
