This is a Dockerfile for building development environment for Trac.

Hopefully people could start developing and tuning Trac related code in 5 minutes, from scratch.

Please note that all Docker commands need **'sudo'** permssion!

**Docker Hub Site**

https://hub.docker.com/r/walty8/docker-trac-dev/


----

**Dependency**
You should have the [docker](https://docs.docker.com/engine/installation/) installed first.


**How to Install:**
- `git clone https://github.com/walty8/docker-trac-dev`
- `cd docker-trac-dev && sudo sh run.sh`

---- 

**Features**
- Latest source code of Trac and Genshi (up to 2016-01-20)
- Ready to run Trac server
- Built-in SSH server
- Two authenticated users (`user1:pass1`, `user2:pass2`)
- A sample subversion reposotiry linked to the sample Trac
- A sample git repository linked to the sample Trac

**Basic Usage**
- Trac server URL: `http://localhost:3080`
- Stop the docker instance: `sudo docker stop trac-dev`
- Restart the docker instance: `sudo docker start trac-dev`
- Remove the docker instance (***caution***): `sudo docker rm trac-dev`

**Development**
- SSH into the docker instance first, `ssh root@localhost -p 3022` (password: `trac`)
- Trac source code is located at `/root/trac-trunk`
- Testing Trac site is located at `/root/test`
- Run unit test: `cd /root/trac-trunk && python -m trac.ticket.tests.batch`
- Modify the source code, for example:
 - `vim /root/trac-trunk/trac/templates/layout.html` (or use any other editor)
 - Replace the line of `Download in other formats` with `Trac Test Modification`.
 - `sh /root/restart_trac.sh`
 - Refresh browser (`http://localhost:3080`) to see the change

**Patch Submission**
- Please read the guideline of [here](http://trac.edgewall.org/wiki/TracDev#Howtogetstarted) first.
- For simple and one-off patch, you might use `git diff` to generate a patch and attach to the ticket.
- For continuous work, you are advised to 
 1. Fork [Trac from github](https://github.com/edgewall/trac)
 2. [Replace the remote repository](http://stackoverflow.com/questions/2432764/change-the-uri-url-for-a-remote-git-repository) of `/root/track-trunk` to your own github project
 3. Commit and push your changes to your own github account.
 3. In the Trac ticket, submit the patch link from github, e.g. https://github.com/edgewall/trac/commit/596b2e72d63a165dd29d85925fce126d3d2cb10d.diff
