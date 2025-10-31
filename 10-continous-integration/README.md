# Github

## GITHUB SHORCUTS

### navigate like a pro

- press ‘?’ on any [github.com](http://github.com) page for a list of shorcuts
- then. hit show all
  ![image.png](attachment:f0661b4e-8b67-4ba1-9900-5ca53fd2a62f:image.png)

## CONTINOUS INTEGRATION

- merging smaller commits frequently, instead of waiting until project is done and doing one big merge
- this means that features can be released quicker!
- CI only works well when there are tests that ensure that new commits didn`t “break the build”
- its even possible to perform a development at the end of a CI build!
  ![image.png](attachment:093cb3c6-d374-40e4-93ec-59c34fad63d1:image.png)

### travis CI integrates with GITHUB

- travis CI is free for open source projects!
- it`s easy to specify what commands you need to run to run tests
- its also easy to test again multiple versions of a language (python2 vs python3) and even multiple version of libraries
- tests run automatically on branches and pull request
- gettting set up is easy:
  - got to travis-ci.org, log in with your gh acct
  - add travis.yml configuration file
  - push to trigger builds

### run tests before merging or accepting PR

![image.png](attachment:aceee70c-380c-4855-94cb-46632b213041:image.png)

### look at build results

- visits travis-ci.org/<username>/<project>
  ![image.png](attachment:6a2d8579-265a-4bd1-bfe8-580001142024:image.png)

### display build status of your project

- add an image to your README to display the build status
- instructions: bit.ly/travis-status
