# Git Gud
## A From Scratch Guide to Git and Github

### Intro
* Firstly if you don't have Git installed, [go install it.](https://git-scm.com/downloads)
* If you are on Windows install the `git-bash` shell when prompted during installation.
  * Git relies on some "unixy" features, and `git-bash` is a bash-esque shell provided by Git out of the box.
* This tutorial assumes a basic knowledge of navigation in a bash terminal.

### Practice setting up your own local repository.
##### So your neighbor Jerry is going through a nasty divorce with his wife Beth. He is having a hard time making friends and you want to help him out by building him a web app called "Friend Finder".
* Create a directory to house our Friend Finder app. This can live anywhere. I am going to create a directory in a dev folder located at _root_ (`~/dev/`):
  ```
  $: mkdir ~/dev/friend-finder
  ```
  ```
  $: cd ~/dev/friend-finder
  ```
* Next, let's initialize an empty git repository. This tells git that there is an active repository on your local machine and its located in your current directory:
  ```
  $: git init
  ```
  * You should see console output from Git saying:
  ```
  Initializing empty Git repository in...
  ````
* Okay great. Now we actually have a working local repo. It ain't much, but it's ours. Now its time to get to work. Let's go ahead and add our first file:
  ```
  $: touch friend-finder.js
  ```
* Wow. What a long day. We made a file. You know what? That's probably enough for now. Jerry will understand. We are at a good solid stopping point and want to save our work without having to remember what we did. Let's commit our code to our local repo.
  * The first step is to double check what changed using `git status`. Consider the possibility that when you went to the bathroom, your annoying friend Tom dropped a file called `totally_not_a_virus.exe` into the project directory and we wouldn't want to save that with all the rest of our work.
  ##### Checking Current Status:
  ```
  $: git status
  ```
  * Git status should have shown you a few different things. First your working branch: `master`, a message saying `Initial commit`, and a section marked: `Untracked files`.
  ##### Staging Changes:
    * Untracked files are files Git doesn't yet know about. That's because we haven't staged our changes yet.
  ```
  $: git add .
  ```
  * Now re-run:
  ```
  $: git status
  ```
  * You should see a section marked `Changes to be committed:` with a reference to our friend-finder.js file. Now your changes are `staged`, meaning they are ready to be committed.
  ##### Committing changes:
  * Now we are going to actually commit our staged changes.
  * `git commit` is the terminal command responsible for committing code. If we pass it the `-m` option, we can add a message.
    * __Commit messages are not optional__.
    * If you run `git commit`, a vi text editor will be launched where you will enter a commit message. By saving and exiting the editor the commit command will be completed.
    * By running `git commit -m`, you may enter a git commit directly in the terminal. The option `-m` flag is the option for "inline message".
  * It's best to follow [Git Community Standards](https://gist.github.com/digitaljhelms/3761873) when committing code. Let's go over a few right now:
    * Commits should be __atomic__, meaning they should contain a specific _focus/purpose_. We should commit _frequently_, and in small _focused chunks_.
      * Think about it this way. No one wants to peer review a commit that contains 147 files with over 1,000 individual changes.
    * Commit messages should be __imperative__. Instead of saying "Added friend-finder.js", the commit messages should use present tense: "Add friend-finder.js"
    * Commit messages should be short, but descriptive:
      * ~~"Add friend-finder.js to the root of the project directory during the initial commit of the Friend Finder App"~~
      * "Add friend-finder.js" or "Initial commit of Friend Finder App"
    * Sadly, we can't always avoid big commits, and sometimes more context is needed in your message. In these cases, provide a summary as the top level commit message, with a longer paragraph underneath detailing the change.
      * This will need to be done in vi by running the default `commit` command without the `-m` flag.
  * Enough talking let's do it:
  ```
  $: git commit -m "Add friend-finder.js"
  ```
  * You should see the following console output:
  ```
  1 file changed, 0 insertions(+), 0 deletions(-)
  ```
    * `0 insertions` meaning no lines of code were added to the file.
    * `0 deletions` meaning no lines of code were removed from the file.
    * This all makes sense, friend-finder.js is an empty file.
  ##### Reviewing Git History
  * You can review the history of your commits using `git log`.
  * This should be pretty self-explanatory. You should see the commit hash, something like:
  ```
  commit 16755ace8a9ea1b59361a2b75c6a586a274ecdcf
  ```
  * This is a unique identifier used to find your commit in the future. For more info on git log and git history, [look here.](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

  ##### Day 2
  * You've come back the next day feeling well rested and ready to get to work. Let's add some code. Paste the following code into `friend-finder.js`:
  ```
  function whatJerryShouldDo() {
    console.log('GET A JOB JERRY!');
  }
  ```
  * Cool. Wow is it lunch already? Let's _stage_ and _commit_ our code.
  ```
  $: git status
  ```
  * At this point friend-finder.js has been modified, but the changes are not yet staged.
  ```
  $: git add .
  ```
  ```
  $: git status
  ```

  * friend-finder.js changes are now staged.

  ```
  $: git commit -m "Add movitational console logs"
  ```

  * Once again the console output will show:

  ```
  1 file changed, 3 insertions(+)
  ```

  * `3 insertions(+)` - We added 3 lines of code, and removed no lines of code, all in a single file.

  ##### Day 3
  * You get back the next morning and realize, you know what? That function is bad. Jerry is a good man who needs my help! So you go back in replace line 2 with:
  ```
    line 02 | console.log('Just be yourself :).');
  ```
  * Now commit your new changes by repeating the steps in day 2 _(with a new commit message)._ You should see the console output the following:
  ```
  1 file changed, 1 insertion(+), 1 deletion(-)
  ```
  * We deleted line 2 and replaced it with a new line.

  ##### Day 4
  * You come into the office only to realize that Jerry's mad-scientist ex-step-father Rick is trying to sabotage your app. And he's done a damn good job. He left his name etched on your desk and your laptop has been covered in some mysterious green goo. You wipe it down and it makes your whole body feel tingly and turns your skin blue temporarily. You try to reboot your computer but to no avail. All your code... is gone.
  * For the sake of this example, let's assume you came back to this document and repeated all these steps. You finally regained all your precious work, but you've lost an entire day. Its now night and you are ready to go home, but you're determined to never let this happen again.
  * Enter Github.
  #### Remote Repositories
  * Thus far we've been committing code to a __local__ repository. It only lives on your local machine. This is a big difference between Git and other Version Control Systems like say SVN. Let's take a minute exploring how SVN works to highlight the differences and importance in the Git Workflow.
    * SVN requires an online connection.
    * When you commit code, your code is pushed to a __centralized__ source code server where everyone else on your team pushes their code as well.
  * Git is __decentralized__.
    * Git does not require an online connection because you must always commit your code to your _local_ repository first _(We never needed the internet to make our commits)_. The workflow looks like:
      * Unstaged Commits --> Local Repository
      * Local Repository --> Remote Repository
    * A decentralized version control system has costs and benefits, but is great for collaboration.
    * When it does come time to _push_ your code to a remote server, Git doesn't seem to care _where_ you want to store your code.
      * You could have one centralized server, like in the above example with SVN, or you could push your code to multiple different servers.
      * Github is the world's largest open source source code repository system. In this example we are going to use Github as our `Remote Repository`. If Rick come back to ruin our code, who cares?
    #### Github Setup
    * [Sign up for Github](https://github.com/) if you haven't already.
    * The most secure way of allowing your local machine to communicate with Github servers is via `SSH`. If you aren't familiar with SSH RSA key pairs here is the highly non-technical TL;DR:
      * SSH RSA key pairs allow your computer to _shake hands_ with a remote server. When the remote server recognizes your key pair, it will _trust_ your computer to push code to it via the SSH protocol. 
    * Github will also allow for your to push your code via `HTTPS`. But because you wont be using a key in this situation, the only way Github will know to trust you is by you manually inputing your username and password each time you push.
    * I recommend following Github's guide for [generating a new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Once you have generated a local ssh key, you will need to [add the public key to your Github account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/).
      * Now that we have taught our computer _how_ to talk to Github, we can create a `Remote Repository` to push our code to.
    #### Creating a Remote Repo
    * Navigate to your Github profile, and then over to the "Repositories" tab. You should see a green 'New' button.
    * Give your remote repo a name. To keep things simple, we will give it the same name we gave the project directory, `friend-finder`.
    * Enter a short description, and we will initialize this repository as a 'Public' repo. Let's skip initializing the repository with a README.
    * Now you should be on your repo's home page. On the right side of the screen you should see a green button labeled 'Clone or download'.
      * From here Git will open a dropdown. At the top of the dropdown you will notice the option to 'use SSH' or 'use HTTPS'. If you skiped generating an SSH key, use HTTPS. In my example I am going to assume you are using SSH.
        * Press the clipboard icon in the dropdown which will copy the address to your clipboard. Something like: `git@github.com:username/your-repo-path`
    * Head on back to your terminal window.
      * Quickly run `git status`. Just to make sure you have no unstaged changes.
      ```
      $: git remote add origin git@github.com:username/your-repo-path
      ```
        * Let's disect that a little bit.
        * `git remote add` - indicates you are setting up a remote repository.
        * `origin` 
          * The word origin here may seem like syntax but it's actually arbitrary. This is simply the name of the remote repo.
          * This could just as easily have been `my_repo` or whatever. Most of the time for most people, they will only have 1 source code server. And in this case we are no exception.
          * The usual standard when dealing with 1 remote repo is to name that repo `origin`. This is what you will see in most cases. So we will settle on `origin`.
        * `git@github.com:username/your-repo-path`
          * This is the address of the remote repo.
          * In this case we see `git@github.com/bla` because we are communicating via the `ssh` protocol.
          * If we were communciating via the `https` protocol we would have seen `https://github.com/bla`.
      * Now run
      ```
      $: git remote -v
      ```
      * `-v` is the flag for `--verbose`. This gives us more information than standard the `git remote` command, which will only lists remote names.
      * You should see this:
      ```
      origin	https://github.com/username/your-repo.git (fetch)
      origin	https://github.com/username/your-repo.git (push)
      ```
      * Looks to me like we are all ready to push our code up to Github.
      ```
      $: git push origin master
      ```
      * Lets take one last second to disect that command.
      * `git push`:
        * When you are first starting out, long after you have closed this Wiki tab, the differences between `git commit` and `git push` can be confusing. So let's beat a dead horse.
          * `git commit` will commit code to your __local repository__.
          * You cannot `git push` _uncommited_ code. Unstaged changes cannot communicate directly to a __remote repository__. Again, Git forces the following workflow:
          * Unstaged changes -> Local Repository
          * Local Repository -> Remote Repository
          * Learn it, live it, love it.
      * `origin`:
        * What we _named_ the remote repository. `origin` corresponds to `git@github.com/username/our-repo.git`.
      * `master`:
        * This is the remote `branch` we are pushing to. We haven't gone over branching yet, but it is an extremely important part of Git and Github. I know I am leaving you in the dark here, but for now let's assume that for the forseeable future we only going to push to one branch: `master`. For the sake of argument, let's assume that by pushing to `master`, you are pushing to the "main" section of your remote repository.
      * Say you had a team mate who came to you and said, "Hey, I just pushed some code up to Github. Want to pull that down so you have it?"
        * Assuming you have no unstaged changes, you could `pull` their code down into your local repo from the remote repo using: `git pull origin master`.

  ##### Wrapping Up:
  * If you refresh Github you should see our `friend-finder.js` file sitting up there on the home page. Spend some time getting familiar with the UI. You can view your `commit history` in the top left, see the timestamp for the last time you committed code, and lots of other useful features.
  * When Rick comes back around to destroy your computer, don't worry. Your code doesn't live in one place anymore. It lives in two. And because Git is _decentralizd_ it can now potentially live in many places.
  * Lastly, there is a lot that we haven't mentioned yet.
  * `Pull Requests` are an important part to working on a team.
  * `Branching` is a great way to push code to a remote repository that isn't quite ready to be merged back in to your "main" `master` branch. `Pull Requests` are requests for someone to review code that sits on a separate branch other than `master`. Once the Pull Request is `approved` the code can then be merged back into `master` and the old branch may be deleted.
  * We haven't gone over `forking`, which is where you actually __clone your own remote repository from another remote repository__. This is an invaluable tool when you need access to external open source packages on Github and either a) don't have time to submit a Pull Request yet or b) are waiting for a Pull Request to be approved but need to use your changes in the mean-time.
    * Please note that a huge part of being a Github user is contributing and giving back. If you think changes to packages need to happen, submit a Github issue or submit a Pull Request. Let the package maintainers and community use your work when possible and applicable.
  * Nevertheless we did what we set out to accomplish. Our code is saved both locally and remotely, in a decentralized manner. We can now code with confidence that we can `revert` to previous commits, or re-pull our code from our remote repository if something goes terribly wrong on our machine.


Thanks for sticking with me and please let me know what I can do to improve this doc. Again this is meant to help beginners who have never used Git or Github before.