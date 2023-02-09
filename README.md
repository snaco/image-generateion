# Image Generation

## Prerequisites

```
pip install diffusers transformers accelerate scipy safetensors torch xformers
```

## Scripts

 * `./generate "prompt1" "prompt2" ... X [--no-cooldown] `

    This can take any number of prompts, make sure each prompt is surrounded by "".  In place of X can be any number, this is how many images to generate per prompt. The `--no-cooldown` option is used to stop the script from checking the gpu temperature before generating. Without this flag the script will pause execution if the temperature is over 75ºC after generating an image. It will wait until the temperature is at 65ºC before resuming generation.

* `./temp` - displays the current gpu temperature