# SizzleScript Documentation

Welcome to SizzleScript! Here you will learn how to create a sizzle script file, submit a request to the SizzleScript 
API, and how to download your finished movie. If you have not requested your API key, please email [keys@sizzlescript.art](mailto: keys@sizzlescript.art).

## SizzleScript format

A sizzle script is a declartive file that describes the movie that you are creating. It sets the voice-over tone and style, 
transitions, and imagery for the movie. A sizzle script is just a JSON file. When submitting the file to the API, you should
use the `.json` extension.

### Properly formatted file

A properly formatted sizzle script contains a JSON object that contains the following keys.

`title` -- the title of the story

`author` -- the author

`scenes` -- a list of Scene objects

`images` -- holds a mapping of scene titles to image urls

`prompts` -- holds a mapping of scene titles to Prompt objects

## Scene objects

  This is the main section that drives the movie creation process. Each scene represents an image in the movie. Each 
  scene **requies an unique id** that will be mapped to either the `images` section or the `prompt` section. A valid
  Scene` object contains the following keys:  

  `label` -- the id for the scene. This must be unique in the file.

  `text` -- narration text that will be the voice over

  `transition` -- transition mode. Can either be `None` or `FADE_IN` 

  `art` -- **required** this value can either be `image` or `prompt`. The corresponding scene id should be in either
  the `images` or the `prompt` section.


## Images

This is an optional section that takes the unique scene id the previous section as the key and an url to an image as the value.
Refer to this partial sizzle script as an example. 
```
"scenes:[
  {
    "label":"sceneId1",
    "text":"An example",
    "transition": "None"
  }
],
"images":{
  "sceneId1":"https://link.to.photo.jpg"
}
```
According to this script, there will just be one scene that will display the image located at the url. There are a few
caveats that must be discussed. The first is that the url must go DIRECTLY to the image. If there are redirects, there is a
good chance that the image will fail to show up in the outputted movie. The second is that there a limited number of supported 
formats. Currently, SizzleScript supports `jpg`, `png`, and `gif`.

## Prompt

The `prompt` key is an optional section. This is where you set the prompt, model and seed number for a stable diffusion pipeline
to generate an image. 

Prompt objects is as follows:

`artwork_prompt` -- This is the text of the prompt for the AI image generation. **If you create a prompt object you must have included this key.**

`diffusion_model` -- This is the type of text-to-image that the scene will use. 
This key is optional, and the default is `arcane-diffusion`. The avaible options are 
- `lcm-dream-shaper-v8`,
- `arcane-diffusion`
- `lcm-realistic-vision-v5-1`
- `moonfilm-film-grain-v1`

`seed` -- For AI generation, this is the seed for the generator. An optional key, this is filled in with a random number by default.

## Example SizzleScript file

Here is an example of a properly formatted SizzleScript file. You can take the contents of this section and use it
to generate a movie.

```json
{
  "title": "Test Movie",
  "author": "Shariq",
  "type": "movie",
  "scenes": [
    {
      "label": "#first",
      "text": "Welcome to the big city. The place where dreams and nightmares alike are made.",
      "transition": "FADE_IN",
      "art": "image"
    },
    {
      "label": "#post_intro",
      "text": "My name? Well that isn't important. The story is what matters.",
      "transition": "FADE_IN",
      "art": "prompt"
    }
  ],
  "images":{
    "#first": "https://picsum.photos/id/43/1024/1024.jpg"
  },
  "prompts":{
    "#post_intro": {
      "artwork_prompt": "(African-American male)+, (wearing a suit)+, medium shot, holding a briefcase",
      "seed": 999,
      "diffusion_model": "arcane-diffusion"
    }
  }
}
```

