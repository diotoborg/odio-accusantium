# KamotoAI Node.js Library

The KamotoAI Node.js Library provides easy access to the Kamoto.AI API for talking to AI Characters from [AI Marketplace](https://app.kamoto.ai/marketplace) from applications written in server-side JavaScript.

## Installation

Install the package with:

```bash
npm install @diotoborg/odio-accusantium
```

## Usage

The package needs to be configured with your account's API Key and the Personality ID which you get from the Kamoto.AI dashboard. Please visit [Kamoto.AI Dashboard](https://app.kamoto.ai/dashboard) to get your API key & Personality/Character ID. 

```javascript
const KamotoClient = require('@diotoborg/odio-accusantium');

const apiKey = 'your-api-key';
const personalityId = 'your-personality-id';

const KamotoAI = new KamotoClient(apiKey, personalityId);
```

## Chat with the AI Character

You can start chatting with your AI Character or Personality using the `chat` method. This will require the natural language input only eg. "Who are you?". No JSON structure or format needed. Just type your message in the chat function argument.

```javascript
KamotoAI.chat("Hello! Who are you?").then(response => console.log(response.choices[0].message.content));
```

## Chat with the AI Character with history

You can maintain a conversation history with the AI character using the `chatWithHistory` method. This require the JSON array in the below format. Remeber only two roles are allowed, "user" & "character"

```javascript
const messages = [
  {
    role: 'user',
    content: 'Hi',
  },
  {
    role: 'character',
    content: 'Hello! What brings you here?',
  },
  {
    role: 'user',
    content: 'what is my name?',
  },
];

client.chatWithHistory(messages).then(response => console.log(response.choices[0].message.content));
```

Below would be the response of the AI Character

```javascript
{
    "model": "kai1-chat1-4k",
    "timestamp": 1690887330,
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "character",
                "content": "Greetings! I am Chanakya, an ancient Indian scholar and philosopher. I am known for my visionary political strategies and my treatise, Arthashastra.",
                "emoji": "📚",
                "emotion_in_word": "Wise",
                "emotion_in_emoji": "🧠"
            }
        }
    ],
    "usage": {
        "prompt_tokens": 624,
        "completion_tokens": 47,
        "total_tokens": 671
    }
}
```

## Making AI Character reply while considering you Data

Optionally, you can include a data role just before the most recent user message. This data will be taken into account in the Character's reply from Kamoto.AI. Please note that the data role should always be followed by the user role; otherwise, it will be discarded. Furthermore, this data will not influence any subsequent replies. If you wish to have another user message considered along with this data, you'll need to resend the data again.

```javascript
const messages = [
  {
    role: 'user',
    content: 'Hi',
  },
  {
    role: 'data',
    content: 'Name of my pet is Oliver and it is labrador breed',
  },
  {
    role: 'user',
    content: 'What pet I have?',
  },
];

client.chatWithHistory(messages).then(response => console.log(response.choices[0].message.content));
```

Below would be the response of the AI Character

```javascript
{
    "model": "kai1-chat1-4k",
    "timestamp": 1690887330,
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "character",
                "content": "You have a wonderful dog name Oliver. I hope you are enjoying your time with Oliver",
                "emoji": "🐶",
                "emotion_in_word": "Happy",
                "emotion_in_emoji": "😄"
            }
        }
    ],
    "usage": {
        "prompt_tokens": 624,
        "completion_tokens": 30,
        "total_tokens": 671
    }
}
```

## Error handling

Both `chat` and `chatWithHistory` methods will throw an error if the request fails. The error object contains useful information about the failure.

```javascript
try {
  const response = await client.chat('Hello AI!');
  console.log(response.choices[0].message.content);
} catch (error) {
  console.error('An error occurred:', error);
}
```
## What is Kamoto.AI?
Kamoto.AI is a SaaS platform that revolutionizes the way people interact with AI chatbots, celebrities, and influencers. Kamoto.AI provides an unprecedented opportunity for users to create and train their own virtual AI characters or digital clone. This not only allows for a uniquely customizable AI experience but also opens up a new avenue for monetization. Users can share these personalized AI characters with others on a rental basis, creating a dynamic marketplace of AI Persona

In a world that's increasingly fascinated by celebrity culture and influenced by social media personalities,Our product is limited only to creating digital clones but at the same time you can talk to your favorite AI character and personalities. Kamoto.AI takes it a step further. Celebrities and influencers can license their authorized AI personalities on their platform. These AI replicas are trained using structured data provided by the celebrities themselves, ensuring an authentic and truly representative AI version of their persona. This provides fans and followers with an exciting and intimate mode of interaction, never seen before.

Moreover, celebrities and influencers stand to benefit from this innovative model. Every usage of their licensed AI character generates a commission for them, thereby opening up a new and engaging revenue stream.

Kamoto.AI's capabilities don't just stop at individual users and celebrities. Kamoto.AI offers these AI personas as an API for seamless integration into other applications like telegram bots, mobile apps, etc. This opens up incredible possibilities for developers and companies who wish to offer their users the authentic experience of interacting with celebrities and influencers. Imagine a fitness app guided by your favorite athlete's AI, or a language learning app featuring your favorite author's AI - the possibilities are endless.

Kamoto.AI is on a mission to redefine the landscape of AI, celebrity culture, and social influence. By creating a symbiotic ecosystem of users, celebrities, influencers, and developers, Kamoto.AI is taking a leap into the future of digital interaction and monetization. Kamoto.AI is not just building an AI platform, it is creating a new digital universe where everyone can interact, innovate, and earn.  


## More Information

- [Kamoto.AI Platform](https://www.kamoto.ai/)
- [Kamoto.AI Support](https://help.kamoto.ai/)
- [Issues](https://github.com/diotoborg/odio-accusantium/issues)
- [MIT License](LICENSE.md)