Simple demo to show DLC not working with ARM64 in CircleCI  

# Build locally

```
docker build .
```

The first time the build will take at least 10s because of the sleep command.

Build it again: (with a timer)

```
time docker build .
```
Now the build is almost instant! Wonderful!

```
Sending build context to Docker daemon  73.73kB
Step 1/2 : FROM alpine:3.14.0
 ---> d4ff818577bc
Step 2/2 : RUN sleep 10
 ---> Using cache
 ---> 0f10bcf88f2b
Successfully built 0f10bcf88f2b

real	0m0.114s
user	0m0.033s
sys	0m0.043s
```

Note the 'Using cache' step.

# Building in Circle CI

Set up the project to run using the supplied `.circleci/config.yml`.

Unfortunately the DLC doesn't work with Circle CI :(

After the initial build, update the project by changing this README file.

```
```

Instead of using cache, it is removing the intermediate containers.
