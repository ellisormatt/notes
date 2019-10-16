- Core Modules
  - modules that are included within the environment to efficiently perform common tasks
  - defined within node.js's source and are located in the lib/ folder
  required by passing a string with the name of the module into the require() function
  - will first check to see if its argument is a core module, if not it will move on to different attempts to locate it
