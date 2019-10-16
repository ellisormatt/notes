- initialize a new repository
  - git init
- adds the file to local staging area
  - git add filename.txt
- see what has been changed in local file
  - git diff filename.txt
- permanently store changes from staging area in a repository
  - git commit -m "these are the changes i made"
- view log of actions on repo
  - git log
- view status of working directory
  - git status

- initial git setup
  - set username
    - git config --global user.name "Matt Ellisor"
  - set email address
    - git config --global user.email "email@example.com"


- saving changes
  - add repo
    - git remote add origin git@github.com:ellisormatt/repo.git
  - push commits to repo
    - got push -u origin master
