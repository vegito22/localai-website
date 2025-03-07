
+++
disableToc = false
title = "Easy Setup - CPU Docker"
weight = 2
+++

We are going to run LocalAI with `docker-compose` for this set up.


Lets clone LocalAI with git.

```bash
git clone https://github.com/go-skynet/LocalAI
```


Then we will cd into the LocalAI folder.

```bash
cd LocalAI
```


At this point we want to set up our `.env` file, here is a copy for you to use if you wish, please make sure to set it to the same as the docker-compose file for later.

```bash
## Set number of threads.
## Note: prefer the number of physical cores. Overbooking the CPU degrades performance notably.
THREADS=2

## Specify a different bind address (defaults to ":8080")
# ADDRESS=127.0.0.1:8080

## Default models context size
# CONTEXT_SIZE=512
#
## Define galleries.
## models will to install will be visible in `/models/available`
GALLERIES=[{"name":"model-gallery", "url":"github:go-skynet/model-gallery/index.yaml"}, {"url": "github:go-skynet/model-gallery/huggingface.yaml","name":"huggingface"}]

## CORS settings
# CORS=true
# CORS_ALLOW_ORIGINS=*

## Default path for models
#
MODELS_PATH=/models

## Enable debug mode
DEBUG=true

## Specify a build type. Available: cublas, openblas, clblas.
# Do not uncomment this as we are using CPU:
# BUILD_TYPE=cublas

## Uncomment and set to true to enable rebuilding from source
REBUILD=true

## Enable go tags, available: stablediffusion, tts
## stablediffusion: image generation with stablediffusion
## tts: enables text-to-speech with go-piper 
## (requires REBUILD=true)
#
#GO_TAGS=tts

## Path where to store generated images
# IMAGE_PATH=/tmp

## Specify a default upload limit in MB (whisper)
# UPLOAD_LIMIT
# HUGGINGFACEHUB_API_TOKEN=Token here
```


Now that we have the .env set lets set up our docker-compose file, this docker-compose file is for CPU Only:

```docker
version: '3.6'

services:
  api:
    image: quay.io/go-skynet/local-ai:master
    tty: true # enable colorized logs
    restart: always # should this be on-failure ?
    ports:
      - 8080:8080
    env_file:
      - .env
    volumes:
      - ./models:/models
    command: ["/usr/bin/local-ai" ]
```


Make sure to save that in the root of the LocalAI folder. Then lets spin up the docker run this in a CMD or BASH

```bash
docker-compose up -d --pull always
```


Now we are going to let that set up, once it is done, lets check to make sure our huggingface / localai galleries are working (wait until you see the ready screen to do this)

```bash
curl http://localhost:8080/models/available
```

Output will look like this:

![](https://cdn.discordapp.com/attachments/1116933141895053322/1134037542845566976/image.png)

Now that we got that setup, lets go download a model by [Downloading]({{%relref "easy-model-import-downloaded" %}}) Or use the [Gallery]({{%relref "easy-model-import-gallery" %}})! 
