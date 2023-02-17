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

 * `./generate "prompt1" "prompt2" ... [--no-cooldown] [[--diffuser=<diffuser_name>] | [--diffuser-flight]] [[--wide=<number>] | [--tall=<number>] | [--width=<number>] [--height=<number>]] [--upscale=<number>] [--count=<number>] [--fast]`

    This can take any number of prompts, make sure each prompt is surrounded by "".
    
    The `--no-cooldown` option is used to stop the script from checking the gpu temperature before generating. Without this flag the script will pause execution if the temperature is over 75ºC after generating an image. It will wait until the temperature is at 65ºC before resuming generation.

    You can specify the resolution with `--height=<number>` and `width=<number>`. When not specified these default to `512`.

    You can specify a diffuser with `--diffuser=<diffuser_name>`. When not provided the diffuser defaults to protogen. Valid choices are:

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

    You can provide `--diffuser-flight` This will override andy `--diffuser` argument and perform the requested generation with each diffuser.

    You can provide `--upscale=<number>` to run the output image through a 2x upscale before it is saved. The number provided is the number of passes to make. I.E: 1 = 2x, 2 = 4x, 3 = 8x.

    You can provide `--wide=<number>` to generate a 16:9 image, manual `--width` and/or `--height` arguments will ignore the `--wide` flag. The `number` is the scale to multiply 18:9 by after i.e. to get a 1920x1080 image you would provide `--wide 15` the script by default starts at (16 * 8)x(19 * 8) since diffusers will throw a fit if the dimensions are not divisible by 8.

    You can provide `--tall=<number>` to generate a 9:16 image. It works the same way as `--wide`

    You can provide `--square=<number>` to generate a scaled 1:1 image. `--square 1` will produce a 512x512 image. The number provided is the multiplier to the side length of the square.

    You can provide `--count=<number>` to generate that many images for each prompt. In the case where `--diffuser-flight` is provided this will generate that many images per propmpt per diffuser.
    
    You can provide `--fast` to generate images faster but at the cost of using much more VRAM. Unless you have a monster GPU it's best to leave this off.

    You can provide `--output-dir=<directory>` to specify where to save the output images. This can be a relative path like `./my/awesome/dir` or an absolute path like `/home/user/even/cooler/dir`

    examples:
    * Generate 3 1920x1080 images, upscaled by 2x of a mouse holding a balloon with the dream2 diffuser
    ```
      ./generate "a mouse holding a balloon, oil painting" --diffuser dream2 --wide 15 --upscale 1 --count 3
    ```
    * Generate an image of batman and an image of coffee with each diffuser
    ```
      ./generate "a steaming hot cup of coffee, digital art" "batman at the disco, cartoon" --diffuser-flight
    ```