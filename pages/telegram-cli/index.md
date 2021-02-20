# Telegram CLI

```bash
timeout 5 telegram-cli -RCDWI --json -e 'history newChan 2' | jq -rR 'fromjson? | .[0].text' | perl -0777 -pe 's|.*Action[^\n]*\n||ig s'

cd /path/to/tg && (sleep 1; echo "contact_list"; sleep 1; echo "msg contact message") | bin/telegram-cli -W -k server.pub
```

##### installation

```bash
apt install snap
snap install telegram-cli
apt install python-dev libpq-dev
python -m pip install --upgrade pip
pip install setuptools_rust
pip install python-telegram-bot --upgrade
```



## Telethon : A Python Based Telegram Client

[Quick-Start — Telethon 1.19.1 documentation](https://docs.telethon.dev/en/latest/basic/quick-start.html)

```python
from telethon import TelegramClient

api_id = 123456789
api_hash = 'XXXX--HASH--XXXX'
client = TelegramClient('anon', api_id, api_hash)

async def main():
    async for message in client.iter_messages('Cornix | Source',limit=20):
        print(message.id, message.text)
with client:
    client.loop.run_until_complete(main())
```

##### installation

```bash
apt update
apt upgrade
rm /usr/bin/python
ln -sv /usr/bin/python3 /usr/bin/python
apt install python3-pip python3-dev libpq-dev
ln -sv /usr/bin/pip3 /usr/bin/pip
apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libsqlite3-dev
pip install wheel setuptools_rust pillow cryptg aiohttp hachoir setuptools telethon
pip install python-telegram-bot --upgrade
```

## Telegram Bot in Python

[Part 1: How to create a Telegram Bot in Python in under 10 minutes | Codementor](https://www.codementor.io/@karandeepbatra/part-1-how-to-create-a-telegram-bot-in-python-in-under-10-minutes-19yfdv4wrq)

[Part 2: Deploying Telegram Bot for FREE on Heroku | Codementor](https://www.codementor.io/@karandeepbatra/part-2-deploying-telegram-bot-for-free-on-heroku-19ygdi7754)

[telegram.ext package — Python Telegram Bot 13.2 documentation (python-telegram-bot.readthedocs.io)](https://python-telegram-bot.readthedocs.io/en/stable/telegram.html)



### References

[Full Emoji List, v13.1 (unicode.org)](http://www.unicode.org/emoji/charts/full-emoji-list.html) Emoji code are used like this:
 `thunderstorm = u'\U0001F4A8'`