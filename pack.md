# Pack Demo

## Requirements

* Docker CLI
* Pack cli
  * [install docs](https://buildpacks.io/docs/install-pack/)

```bash
# Installing pack on mac os
brew tap buildpack/tap
brew install pack
```

* Github Repos
  * [spring-music](https://github.com/cloudfoundry-samples/spring-music)
  * [spring pet shop](https://github.com/spring-projects/spring-petclinic)
  * [buildpack samples](https://github.com/buildpacks/samples)
  * Coming soon, a useful go web app

## Build spring-music

In order to show a bit of what pack can do we're going to package up and run spring-music locally.

```bash

# Investigate buildpacks

pack suggest-builders

# for our sample app we can pick any of them
# luckily we're cool so we're going to pick the cloudfoundry/cnb:cflinuxfs3 builder

pack set-default-builder cloudfoundry/cnb:cflinuxfs3

# clone spring music
git clone https://github.com/cloudfoundry-samples/spring-music

# Do a simple local build

cd spring-music
pack build jasonmorgan/spring-music # note I used my docker registry prefix so I can publish it later

# watch the exciting output
# ooooooohhhhh
# aaahhhhhh

## checkout your new image

docker images

## Examine the output for your new spring-music container

## Run the image

docker run -p 8080:8080 jasonmorgan/spring-music

## browse to your new web app at localhost:8080
## use ctrl + c to breakout of your container

```

## Build and publish

Same as the workflow above but this time we're going to publish our image to the docker registry

```bash

# from the spring-music directory
pack build jasonmorgan/spring-music --publish

## go ahead and take a look at your newly published image

```

That's all for now, if you're building a golang app be sure you have a go.mod file or the builder won't recognize what it is.
