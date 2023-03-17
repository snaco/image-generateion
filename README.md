# Image Generation

## Prerequisites

Install python 3.10.6 then run
```
pip install pipenv
pipenv install
pipenv shell
```

When starting a new session, make sure to run `pipenv shell` to actiate the pip environment. 

## Scripts
  * `./temp` - displays the current gpu temperature

 * `./generate` - begins image generation based on the config settings in `config.yml` this is also where prompts and negative prompts are set.

## Available Diffusers
  These are the pre-loaded diffusers the sctipt supports, you can add any diffuser you would like to use from huggingface to the `diffuser_names` dictionary in the generate script. the key is a shorthand that you can use in the config.yml and the value is the full diffuser identifier which is used to pull the diffuser from huggingface.

  * `sd2` - stabilityai/stable-diffusion-2-1
  * `er` - nitrosocke/elden-ring-diffusion
  * `epic` - johnslegers/epic-diffusion-v1.1
  * `dream1` - dreamlike-art/dreamlike-diffusion-1.0
  * `dream2` - dreamlike-art/dreamlike-photoreal-2.0
  * `protogen` - darkstorm2150/Protogen_Infinity_Official_Release
  * `nitro` - nitrosocke/Nitro-Diffusion
  * `lowpoly` - MirageML/lowpoly-world
  * `sci-fi` - Joeythemonster/sci-fi-landscape
  * `waifu` - hakurei/waifu-diffusion

## Config
  The config has comments on each property to explain their use.