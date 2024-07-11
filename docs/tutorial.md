# Getting Started

First, you will need get an API key by emailing [keys@sizzlescript.art]("mailto: keys@sizzlescript.art"). After you have
that you will need an API client, like Postman or Bruno. Over here we love Bruno, so we will use that in our example.

## The SizzleScript

Everything begins with the sizzlescript, a JSON file that tells the API what to render in the final movie. You can learn more 
about the inner workings of a sizzlescript file here, but for now let's use this as an example. Copy the section below 
into a file and give it the '.json' extension.

```
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
      "text": "In my line of work, I tend to travel. Not in physical space; but in cyber space.",
      "transition": "FADE_IN",
      "art": "prompt"
    }
  ],
  "images":{
    "#first": "https://picsum.photos/id/43/1024/1024.jpg"
  },
  "prompts":{
    "#post_intro": {
      "artwork_prompt": "Cyberpunk computer terminal on a desk, lofi, medium shot",
      "seed": 999,
      "diffusion_model": "arcane-diffusion"
    }
  }
}
```

