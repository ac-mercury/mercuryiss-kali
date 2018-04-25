Disposable Kali Linux containers for Mercury ISS / pentesting engagements.
**Remember: containers don't offer the same level of host isolation as virtual machines.**

Feedback and pull requests are welcome!

# Starting the Kali environment
  - `./start.sh container-name /path/to/data /path/to/scripts /path/to/installers`
  - Hack away
  - `/tmp/.docker.xauth` may have to be removed to restart the container in the event of a new X session.
 
# Useful Docker commands
  - `Ctrl + P + Q` - from within container, detach and leave it running
  - `sudo docker ps -as` - list running docker containers
  - `sudo docker attach <container>` - attach to container again
  - `sudo docker exec -it <container> sh -c "stty cols $(tput cols) rows $(tput lines) && bash" ` 
     start another bash process within the container
  - `sudo docker stats [container]` - container resource usage

# TODO
  - SPARTA - X11 issues
  - postgresql persistence for metasploit 
  - environment file configuration
  - netselect-apt configuration for fast package mirror installation

BSD 2-Clause License

Copyright (c) 2018, mercuryiss-kali Maintainers
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

