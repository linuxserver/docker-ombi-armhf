[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://ombi.io/
[hub]: https://hub.docker.com/r/lsioarmhf/ombi/

THIS IMAGE IS DEPRECATED. PLEASE USE THE MULTI-ARCH IMAGES AT `linuxserver/ombi`

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/ombi
[![](https://images.microbadger.com/badges/version/lsioarmhf/ombi.svg)](https://microbadger.com/images/lsioarmhf/ombi "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/ombi.svg)](https://microbadger.com/images/lsioarmhf/ombi "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/ombi.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/ombi.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/armhf/armhf-ombi)](https://ci.linuxserver.io/job/Docker-Builders/job/armhf/job/armhf-ombi/)

[hub]: https://hub.docker.com/r/linuxserver/ombi/

So what is [Ombi][appurl] you ask!?

Ombi allows you to host your own Plex Request and user management system.
 
If you are sharing your Plex server with other users, allow them to request new content using an easy to manage interface! 

Manage all your requests for Movies and TV with ease, leave notes for the user and get notification when a user requests something. 

Allow your users to post issues against their requests so you know there is a problem with the audio etc. 

Even automatically sent them weekly newsletters of new content that has been added to your Plex server!

[![ombi](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/ombi.png)][appurl]

## Usage

```
docker create \
  --name=ombi \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<timezone> \  
  -p 3579:3579 \
  lsioarmhf/ombi
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 3579` - the port(s)
* `-v /config` - where ombi should store config files.
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it ombi /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Webui is at `<your-ip>:3579`, Follow the setup wizard on initial install.  Then configure the required services.

## Updating to Ombi v3

This image now contains Ombi v3. The settings and database from v2 are not compatible with v3 and existing users will have to set up v3 from scratch. However, the v2 settings and database will be preserved. Users wishing to remain on or go back to v2 with existing data can pull the image tag `lsioarmhf/ombi:v2` but keep in mind that it will no longer receive any updates.

## Info

* Shell access whilst the container is running: `docker exec -it ombi /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f ombi`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' ombi`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/ombi`

## Versions

+ **09.01.19:** This image is deprecated. Please use the multi-arch images at linuxserver/ombi
+ **11.03.18:** Add HOME env to Dockerfile.
+ **05.03.18:** Switch to Ombi v3 stable based on .net core. V3 uses a different database structure so the user has to set up from scratch again. V2 settings are not lost by updating; the user can go back to v2 with old settings and data by pulling image tag `v2`
+ **26.01.18:** Fix continuation lines.
+ **19.04.17:** Switch to using inhouse mono baseimage.
+ **13.02.17:** Spec to latest X86.
+ **14.01.17:** Initial Release Date.
