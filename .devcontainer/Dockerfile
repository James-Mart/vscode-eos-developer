###############################################################
##########     NO EDITS ARE NEEDED IN THIS FILE    ############
###############################################################

# specify the node base image with your desired version node:<version>
FROM node:17

# Saw online:
RUN apt-get update                  \
    && apt-get clean                \
    && apt-get -y install sudo      \
    && rm -rf /var/lib/apt/lists/*  \
    && npm install -g yo generator-code

RUN useradd -ms /bin/bash yo
RUN echo "yo:yo" | chpasswd && adduser yo sudo
RUN chown yo /home/yo

USER yo

WORKDIR /home/yo

# Use bash shell - Needed to use ansi-c quotes
SHELL ["/bin/bash", "-c"]

# Some nice-to-haves when using git inside the container
RUN echo $'\n\
parse_git_branch() {\n\
  git branch 2> /dev/null | sed -e "/^[^*]/d" -e "s/* \\(.*\\)/ (\\1)/"\n\
} \n\
export PS1="\u@\h \W\[\\033[32m\\]\\$(parse_git_branch)\\[\\033[00m\\] $ "\n\
if [ -f ~/.git-completion.bash ]; then\n\
  . ~/.git-completion.bash\n\
fi\n\
' >> /home/yo/.bashrc

