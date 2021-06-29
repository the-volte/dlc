Simple demo to show DLC not working with ARM64 in CircleCI  

# Build locally

```
docker build .
```

The first time the build will take at least 20s because of the sleep commands.

Build it again with the same command:

```
docker build .
```

Now the build is almost instant! Wonderful!

```
Sending build context to Docker daemon  94.72kB
Step 1/4 : FROM alpine:3.14.0
 ---> d4ff818577bc
Step 2/4 : RUN sleep 5
 ---> Using cache
 ---> 44883d187f44
Step 3/4 : RUN sleep 5
 ---> Using cache
 ---> 259cd6268bc9
Step 4/4 : RUN sleep 10
 ---> Using cache
 ---> e22ad582adf0
Successfully built e22ad582adf0
```

Note the 'Using cache' steps.

# Building in Circle CI

Set up the project to run using the supplied `.circleci/config.yml`.

Unfortunately the DLC doesn't work with Circle CI :(

```
Sending build context to Docker daemon     64kB
Step 1/4 : FROM alpine:3.14.0
3.14.0: Pulling from library/alpine

Digest: sha256:234cb88d3020898631af0ccbbcca9a66ae7306ecd30c9720690858c1b007d2a0
Status: Downloaded newer image for alpine:3.14.0
 ---> b0e47758dc53
Step 2/4 : RUN sleep 5
 ---> Running in 0ad32ebd9115
Removing intermediate container 0ad32ebd9115
 ---> b74f02c5d5be
Step 3/4 : RUN sleep 5
 ---> Running in 7a6f08f81eee
Removing intermediate container 7a6f08f81eee
 ---> 6aa20dfdf89e
Step 4/4 : RUN sleep 10
 ---> Running in 77eb8a429c17
Removing intermediate container 77eb8a429c17
 ---> ee1f02f66546
Successfully built ee1f02f66546
Successfully tagged *************************************************/dlc:latest
CircleCI received exit code 0
```

Instead of using cache, it is removing the intermediate containers.
