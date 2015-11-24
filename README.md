# Masked Priming Suite

This app is being designed as a successor to the [DMDX app for measuring reaction times to visual and auditory stimuli](http://www.u.arizona.edu/~kforster/dmdx/dmdx.htm). DMDX was built during a time when the physical hardware was a significant limiting factor in the design. Today, however, the ubiquity of fast computing has made it possible to reproduce the quality and accuracy of the testing suite while using modern higher-level software techniques. This app is designed to maximize two goals:

 - Make it easy for researchers to build experiments
 - Operate universally on multiple platforms

The first goal means that the idioms used to generate the sequence of testing steps should be simple to recognize without having to learn a complicated system. The _item files_ used by DMASTR and DMDX are somewhat arcane albeit powerful in their syntax. A proper redesign might be able to trade some of the terseness of the item file with a verbosity that expresses the intent of each step more clearly. The usefulness of any such redesign would of course have to outweight the familiarity of researchers in the field with the existing synax.

The second goal will inform the choice of language and platform used to design the app. Today, this universality comes unquestionably through the Web using HTML, JavaScript, and CSS. Modern extensions to the JavaScript language, such as the `performance.now()` high-precision timer and the `requestAnimationFrame()` function provide even higher levels of accuracy and control than the former DirectX environment used in DMDX. Further, the JavaScript _EventLoop_ provides an obvious and pain-free way of interacting with user input. Properly designed, this app should run just as seamlessly in a mobile browser as it does in a desktop browser, or even on such platforms as a desktop app via [Electron](http://electron.atom.io).
