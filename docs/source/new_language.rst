Adding a new programming language
=====================================

One of the key capabilities of the Runestone system is being able to interactively execute and manipulate code within its textbooks. Developers may wish to add new programming languages to the system. Doing so requires making changes in a number of places. This section describes where these changes need to be made, as well as recommendations on how to do so.

Jobe
----
Jobe is the server that receives and executes programming code.

Changes to the Jobe repo
++++++++++++++++++++++++

 The `original project  <https://github.com/trampgeek/jobe>`_ continues to be developed, but Runestone is based on a `fork of that project <https://github.com/RunestoneInteractive/jobe>`_ that was made in 2023. Updates to Jobe should be made on the Runestone fork. Therefore, make your own personal fork of the `Runestone Jobe repo <https://github.com/RunestoneInteractive/jobe>`_, and make your updates there.

The main change necessary is to create a new PHP task file. Task files exist for each of the built-in languages, and are found in the ``libraries`` directory. The simplest approach is likely to find a task file for a language that is similar to the language that you will be adding, and modify it accordingly. Jobe will automatically discover this file once you have created it; there is no need to otherwise register the new language.

The other change you should make is to the ``testsubmit.py`` file, which includes tests for all of the languages that Jobe supports. Add similar tests for your new language to those that are already there.

Changes to the rs repo
++++++++++++++++++++++


Once you have made your changes, you will want to locally test them. To do so, you can start Jobe in a local webserver. Runestone does this as part of its polylith architecture, but you may find it simpler to start up Jobe as a completely standalone server while you are creating and testing the above updates. These instructions are You can do this via the `JobeInABox <https://github.com/trampgeek/jobeinabox>`_ project, which is a Docker container that runs Jobe within. Clone the JobeInABox repo, and then make two changes to `Dockerfile`:
* Find the line that begins with `git clone`, and change it to pull Jobe from your forked version rather than the original.
* Add whatever content you need to install your new programming language. This is easiest if you can just add packages to the `apt-get` command, but you might have to do more.