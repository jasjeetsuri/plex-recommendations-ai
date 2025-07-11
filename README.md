# Plex Recommendations AI

This project involves creating a 'Recommended' collection on your Plex server using the power of OpenAI. 
By analyzing your unique watch history, it will provide you with personalized suggestions that perfectly align with your preferred genre. 
With this feature, you'll easily discover a handful of delightful recommendations from your extensive movie list, making it a breeze to find your next enjoyable watch!

## Features

- Auto create/update a plex movie and tv collections per user.
- Dynamic results based on ChatGPT results and Plex watch history.
- Creates a short description on the plex collection describing why it chose them movies.

![image](https://github.com/user-attachments/assets/bb0f0da7-baf5-466a-836b-618c3a14edde)

![image](https://github.com/user-attachments/assets/b87b846e-f6a1-4344-af0f-38953fcf4d3d)

## Notice!!

Since this links into your OpenAI account there will be some cost with each query to ChatGPT, so make sure you keep an eye on it!

Check your usage here: https://platform.openai.com/account/usage

Personally for me so far it's been' $0.01 a day to run since it's only using ChatGPT 3.5 and running once a day.

Changing `SECONDS_TO_WAIT` to run too often will obviously increase the costs as more queries will happen.

## You'll need

- Plex server host and port
- Plex token
- Open AI account and key - Can be obtained from their website.
- Docker setup

## Setup

You'll need docker set up on your server and to best way to run this is through docker-compose.

Replace all instances of "safetyp1" with yoir username in ```main.py```.

Build the docker image
```sudo docker build -t plex-ai .```

Use this example below:

```yaml
version: "2.1"
services:
  plex-recommendations:
    image: plex-ai
    container_name: plex-recommendations
    environment:
      - PLEX_URL=<local plex url>
      - PLEX_TOKEN=<plex token>
      - OPEN_AI_KEY=<open ai key>
      - LIBRARY_NAMES=Movies, TV Shows
      - COLLECTION_TITLE=<title>
      - HISTORY_AMOUNT=<amount> # How far it will look into your plex watch history
      - RECOMMENDED_AMOUNT=<amount> # How many recommendations it will request
      - MINIMUM_AMOUNT=<amount> # The minimum amount of matches it will need to create the collection
      - SECONDS_TO_WAIT=<amount> # How long in seconds it will wait to call again (default: 86400)
      - ADD_TO_WATCHLIST=0
      - CREATE_COLLECTIONS=
    restart: unless-stopped
```
## Stuff to do
- Allow matching data past 2021?
