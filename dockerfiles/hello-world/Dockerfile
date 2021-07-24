# "as base" means to create a stage 
# This isn't compulsory, but it lets me set a point that future sets of commands in this build can run off
# It also gives me a target I can set in my build command; if I only want to build up to a certain point I can do that
FROM alpine:3.14 as base

# RUN command to install a basic package from apk (Alpine package manager)
FROM base as fortune
RUN apk update && apk add fortune

# COPY to add a basic file in. Syntax is COPY <source> <destination>
# Source path is relative to build context passed in
# Can also copy in files from previous stages by setting --from
FROM base as copyfiles
COPY cowtext.txt /usr/cowtext.txt

# Grab a package called Cowsay and run it, pull in the file we added in that copyfiles step
FROM copyfiles as cowsay
RUN apk update && \
    apk add --no-cache git perl && \
    cd /tmp && \
    git clone https://github.com/jasonm23/cowsay.git  && \
    cd cowsay ; ./install.sh /usr/local && \
    rm -rf /var/cache/apk/* /var/tmp/* /tmp/* && \
    apk del git

# I could also use CMD here. The difference is that ENTRYPOINT is always run, while CMD is only run when I don't pass in another command to run
# The more usual approach here is to use ["executable", "parameter"] but that will fail 
ENTRYPOINT "cowsay" $(cat /usr/cowtext.txt)
