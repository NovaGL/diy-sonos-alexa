# DIY Sonos on Alexa
This project is for connecting Sonos to Alexa.

It uses several tools to achieve this

- Bespoken Tools
- Sonos-HTTP-API
- Node-Red

It is a do it yourself tool that allows you to control a Sonos speaker without an AWS setup.

You still need to be setup as a developer and create a skill.

Instead of linking it to AWS you link it to your webhook on your local server using BST Proxy (Bespoken Tools)

There are two files.

- Flow to import into Node-Red. Change the settings to suit your enviroment
- Skill for Alexa change the HTTP adddress to point to your BST setup

The vast majority of commands that you would want to do via Alexa can be done through this skill.

### BST Proxy Setup
Download BST proxy from here https://github.com/bespoken/bst

Once downloaded type ```bst proxy http 1880``` in the console to start the proxy.
Use your own method to keep the Node alive. I use PM2.

### Node-Red Setup

Import the ```node-red-flow.json``` file to setup the below
Here is the setup for Node-Red in the Global Settings change node

| Intent        | Example Utterance |
| ------------- | ------------- |
|msg.zone       | This is the name of the player you want to control|
|msg.ip         |this is the ip with port number of the node Sonos-HTTP-API installation|
|msg.min_volume |The lower limit that you want Alexa to be able to control volume to|
|msg.max_volume |The upper limit that you want Alexa to control the volume to|


### Alexa Setup
Create a new skill and import the intents from the ```Alexa-intents.json``` file
The configuration endpoint is the BST address when you run BST proxy on your machine it should be something like this

Your URL for Alexa Skill configuration:
https://proxy.bespoken.tools/sonos?node-id=[copy-id-here]


### Information Commands
| Intent        | Example Utterance |
| ------------- | ------------- |
|Now Playing|What Song is Playing|
|list players|What are my Players|


### General Commands
| Intent        | Example Utterance |
| ------------- | ------------- |
|Play\Pause\Previous\Next|Play Music\ Pause \ Previous\ Next track|
| Repeat On\Off  | Turn on Repeat  |
| Shuffle On\Off  |Turn on Shuffle  |
|Volume\Mute| Set Volume to % \ Lower Volume \ Increase Volume|
|Clear Queue|Clear the Queue|

### Search Commands
| Intent        | Example Utterance |
| ------------- | ------------- |
|Play track\album\artist|Play Album 21|
|Play track\artist\album\playlist on source|Play Hot Hits Australia playlist on Spotify|
|Favorite [id] or Favorite[name]| Play favorite 1 or Play Favorite Dance Music|
