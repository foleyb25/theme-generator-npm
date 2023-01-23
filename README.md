# oai-theme-generator

## Overview
oai-theme-generator npm package utilizes the Text Completion and Image generation Libraries from OpenAI. The package takes one required parameter, the OpenAI api key, and generates a color scheme as well as an image. It is recommended you give a textCompletionPrompt as well as a colorGenerationPrompt or you will be returned an 80s theme. You've been warned.

## Usage

```javascript
const ThemeGenerator = require('oai-theme-generator')

const textCompletionPrompt = 'Human: Write me a prompt for An AI art generator. Generate a prompt that is based on the 1980s in the United States',
const colorGenerationPrompt = 'Human: Give me a color scheme representing the 1980s in the United States. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'

const options = {
    openAIKey: process.env.OPENAI_API_KEY,
    imageGenerationPrompt: imageGenerationPrompt,
    colorGenerationPrompt: colorGenerationPrompt
}

const tg = new ThemeGenerator(options)

const themeData = await tg.start()

console.log(themeData)
```

Here is what the output will look like:

```javascript
{
        colors: {
            primary: '#E6F1FE',
            secondary: '#FFFBF9',
            tertiary: '#D8F7FF',
            one: '#00A2E8',
            two: '#FFB000',
            three: '#000000',
            four: '#FE7A15',
            five: '#F3F3F3'
        },
        imageUrl: 'https://oaidalleapiprodscus.blob.core.windows.net/private/org-DTAU4THvdIQUI5xyxSYHxNI7/user-x5DaR3qcy8hDSFwmbFupi5CD/img-BmRqJhXgwoEBMvIoKh5V9FHy.png?st=2023-01-22T19%3A34%3A14Z&se=2023-01-22T21%3A34%3A14Z&sp=r&sv=2021-08-06&sr=b&rscd=inline&rsct=image/png&skoid=6aaadede-4fb3-4698-a8f6-684d7786b067&sktid=a48cca56-e6da-484e-a814-9c849652bcb3&skt=2023-01-22T18%3A48%3A51Z&ske=2023-01-23T18%3A48%3A51Z&sks=b&skv=2021-08-06&sig=UifRV9JfggnaNGqpSCgSTCqbBRD17W92Gz6QfB3ENJ8%3D',
        prompt: "AI Art Generator Prompt: Create a modern take on a '80s pop culture icon that reflects the vibrant and retro aesthetics of the decade."
}
```

Notice the prompt is different in the output than the one you input. This is because we are getting a random prompt generated by the bot, which is then passed to the image generator. This is to provide more randomness and automated creativity.

## Limitations

### Set to return 8 colors

As of now, it's set to create 8 and exactly 8 colors for the color scheme. If the AI does not return 8 colors as specified, the request will fail. Simple fix will be implemented soon.

### Image Retrieval Authentication issues

The image url that is returned from OpenAI is good for a limited amountj of time then Authentication issues happen. The developer will need to download the image and save it in their own form of storage. Image compression is needed as well.

## Future Implementations

### Fine tune the inputs 

Instead of writing out an entire string for inputs, the user/developer can provide required inputs which will be interpolated into the string. For example:

Required params:
numColors
ThemeEra

which can be interpolated into the string like so:

```javascript
'Human: Give me a color scheme representing ${ThemeEra}. give me the colors in Hex Values and give me ${numColors} colors'
```

### Specify image dimensions inputs

Give the user the ability to specify the image size returned. The size of the image right now is around 3 mb and reducing the dimensions would help with load times.

## Examples

Inputs:
```javascript
const textCompletionPrompt = 'Human: Write me a prompt for An AI art generator. Generate a prompt that is based on the 1980s in the United States',
const colorGenerationPrompt = 'Human: Give me a color scheme representing the 1980s in the United States. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'
```

Output:
![1980s generated theme](https://raw.githubusercontent.com/foleyb25/theme-generator-npm/main/images/1980s.png)

Inputs:
```javascript
const imageGenerationPrompt = 'Human: Write me a prompt for an AI art generator. Write a prompt that is based on the 1800s classical era in the europe'
const colorGenerationPrompt = 'Human: Give me a color scheme representing the 1800s classical era in Europe. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'
```

Output:
![Classical 1800s era generated theme](https://raw.githubusercontent.com/foleyb25/theme-generator-npm/main/images/classical_1800s.png)

Inputs:
```javascript
const imageGenerationPrompt = 'Human: Write me a prompt for an AI art generator. Write a prompt that is based on the emo punk rock phase of the early 2000s era in the united states'
const colorGenerationPrompt = 'Human: Give me a color scheme representing the early 2000s era emo punk rock phase in the United States. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'
```

Output:
(fitting!)
![emo 2000s generated theme](https://raw.githubusercontent.com/foleyb25/theme-generator-npm/main/images/emo_2000s.png)

Notice the text on my application does not change with the theme. This is definitely do-able.

Inputs:
```javascript
const imageGenerationPrompt = 'Human: Write me a prompt for an AI art generator. Write a prompt that is based on prohibition and gangsters of chicago.'
const colorGenerationPrompt = 'Human: Give me a color scheme representing prohibition and gangsters of chicago. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'
```

Output:
![Prohibition and Chicago generated theme](https://raw.githubusercontent.com/foleyb25/theme-generator-npm/main/images/prohibition_chicago.png)

Inputs:
```javascript
const imageGenerationPrompt = 'Human: Write me a prompt for an AI art generator. Write a prompt that is based on the roaring 1920s era in the united states'
const colorGenerationPrompt = 'Human: Give me a color scheme representing the roaring 1920s era in the United States. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'
```

Output:
![Roaring 20s generated theme](https://raw.githubusercontent.com/foleyb25/theme-generator-npm/main/images/roaring_20s.png)

Inputs:
```javascript
const imageGenerationPrompt = 'Human: Write me a prompt for an AI art generator. Write a prompt that is based on woodstock music festival in 1969.'
const colorGenerationPrompt = 'Human: Give me a color scheme representing Woodstock music festival in 1969. give me the colors in Hex Values and give me 8 colors, the first 3 I can use for a background and the other 5 for styling'
```

Output:
![Woodstock 69 generated theme](https://raw.githubusercontent.com/foleyb25/theme-generator-npm/main/images/woodstock_69.png)