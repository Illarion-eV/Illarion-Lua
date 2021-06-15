# Tutorial

This tutorial shows how to get started with Illarion content development. It gives a basic introduction into our development process and policies, i.e. what you need to know to contribute to Illarion development. We will go through the steps to set up a development environment and show how projects (even small ones, like fixing spelling errors) are started and shared.

Should you encounter any problems with this tutorial, please do not hesitate to ask for help on [Discord](https://illarion.org/community/us_chat.php). Feedback and suggestions on how to improve it are also welcome!

## Initial Setup

1. Create a free [GitHub](https://github.com) account if you don't have one and verify your email address.
2. [Fork](https://github.com/illarion-ev/illarion-content/fork) the Illarion game content to your GitHub account.
3. [Fork](https://github.com/illarion-ev/illarion-map/fork) the Illarion maps to your GitHub account.
4. Install and run [Visual Studio Code](https://code.visualstudio.com).
5. Select _Source Control_ on the left tool bar, then _Clone Repository_ and _Clone from GitHub_. ![](images/tutorial/clone.png)
6. Authorize Visual Studio Code to access GitHub.
7. In Visual Studio Code, select the Illarion-Map repository and afterwards a location to save it to. Make sure the folder is open in Visual Studio Code.
8. Select _Source Control_ again. Select _... > Remote > Add Remote..._, insert `https://github.com/Illarion-eV/Illarion-Map` and name it _upstream_. If asked, you can choose to periodically run `git fetch`. ![](images/tutorial/remote.png)
9. On the bottom blue bar, click the current master branch and select _origin/develop_. ![](images/tutorial/branch.png)
10. Select _File > Close Folder_ and repeat steps 5, 7, 8 and 9 for the Illarion-Content repository, using `https://github.com/Illarion-eV/Illarion-Content` as remote URL. Name the remote _upstream_ as well.
11. Close the Illarion-Content folder and re-open it. You will be asked to install recommended extensions. Do so. These extensions will offer better support for Lua, Git and point out problems in your Lua code. ![](images/tutorial/extensions.png)
12. Every change you make needs a name and an email. Use a name Illarion devs know you by and an email you can be reached at:
    1. From the menu select _View > Terminal_.
    2. Enter: `git config --global user.name "your name here"`
    3. Enter: `git config --global user.email your@email.here`
13. Setup the [local Illarion development server](https://github.com/Illarion-eV/Illarion-Dev). Use your Illarion-Map and Illarion-Content directories under 2. Setup.

## Starting a Project

1. Make sure the Illarion-Content folder is open and the bottom blue bar shows _develop_.
2. Select _Source Control_ on the left tool bar and select _... > Pull, Push > Pull from... > upstream > upstream/develop_.
3. Select _develop > Create new branch..._ and name it _feature/hello-illarion_. Notice that the blue bar shows the new branch.
4. Select _Explorer_ on the left bar and open _server > login.lua_.
5. Find the line `function M.onLogin(player)` and under it enter `player:inform("Hello Illarion Development!")`
6. Save the file.
7. Start your local server and connect with your Illarion client to check for the new login message. ![](images/tutorial/hello.png)
8. Under _Source Control_ you can now see login.lua as a modified file. Click + to stage the changes. login.lua will now show under _Staged Changes_.
9. Enter a message title "Say hello on login", insert a blank line and write a more detailed message below. Press CTRL + Enter to submit the commit.
10. Under _Source Control_ select _... > Push_ to send your changes to your GitHub repository.

## Sharing your Work

1. On GitHub go to your Illarion-Content repository and in the left-hand combo box select the new _feature/hello-illarion_ branch. ![](images/tutorial/github.png)
2. Either click _Compare & pull request_ or _Contribute > Open pull request_.
3. Switch the base branch from _master_ to _develop_.
4. Enter a suitable title and description before **not** clicking _Create pull request_, as this would notify a lot of developers and this is not a real project.