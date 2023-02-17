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

 * `./generate "prompt1" "prompt2" ... X [--no-cooldown] [[--diffuser <diffuser_name>] | [--diffuser-flight]] [[--wide <number>] | [--tall <number>] | [--width <number>] [--height <number>]] [--upscale <number>] [--count <number>]`

    This can take any number of prompts, make sure each prompt is surrounded by "".  In place of X can be any number, this is how many images to generate per prompt. 
    
    The `--no-cooldown` option is used to stop the script from checking the gpu temperature before generating. Without this flag the script will pause execution if the temperature is over 75ºC after generating an image. It will wait until the temperature is at 65ºC before resuming generation.

    You can specify the resolution with `--height <number>` and `width <number>`. When not specified these default to `512`.

    You can specify a diffuser with `--diffuser <diffuser_name>`. When not provided the diffuser defaults to protogen. Valid choices are:
    * `sd2` - stabilityai/stable-diffusion-2-1
    * `er` - nitrosocke/elden-ring-diffusion
    * `epic` - johnslegers/epic-diffusion-v1.1
    * `dream1` - dreamlike-art/dreamlike-diffusion-1.0
    * `dream2` - dreamlike-art/dreamlike-photoreal-2.0
    * `protogen` - darkstorm2150/Protogen_Infinity_Official_Release
    * `nitro` - nitrosocke/Nitro-Diffusion
    
    You can provide `--diffuser-flight` This will override andy `--diffuser` argument and perform the requested generation with each diffuser.

    You can provide `--upscale <number>` to run the output image through a 4x upscale before it is saved. The number provided is the number of passes to make. I.E: 1 = 2x, 2 = 4x, 3 = 8x. This will run out of memory fast, so sticking to 3 or lower is recommended.

    You can provide `--wide` to generate a 16:9 image (height=504 width=896), manual `--width` and/or `--height` arguments will ignore the `--wide` flag.

    You can provide `--count <number>` to generate that many images for each prompt. In the case where `--diffuser-flight` is provided this will generate that many images per propmpt per diffuser.
    
    examples:
    * Generate 3 16:9 upscaled images of a mouse holding a balloon with dream2 diffuser
    ```
      ./generate "a mouse holding a balloon, oil painting" --diffuser dream2 --wide --upscale 1 --count 3
    ```
    * Generate an image of batman and an image of coffee with each diffuser
    ```
      ./generate "a steaming hot cup of coffee, digital art" "batman at the disco, cartoon" --diffuser-flight
    ```