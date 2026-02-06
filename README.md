A simple Discord bot written in Python that serves as an alarm bot that mentions a user at times specified in a config file. The user may acknowledge alarms by reacting to the message.

It also includes support for snoozing (an additional message sent at an interval if the user hasn't acknowledged the alarm). 

## My Motives
I made this bot for a friend to help her remember when to take her medicine and drink water. I just figured I'd release the source code here and document it since it was a small and fun project to make :)

## Installing & Running
First, you'll want to clone the project using Git and ensure Python 3 is installed.

```bash
# Install required packages.
sudo apt install -y git python3 python3-pip python3-venv

# Clone project
git clone https://github.com/gamemann/discord-alarm-bot

# Change directory to project.
cd discord-alarm-bot/

# Create a virtual environmental at ./venv/
python3 -m venv venv

# Source and initialize the new Python environment.
source venv/bin/activate

# Install requirements from requirements.txt.
# We do this inside of a virtual Python environment so we don't break system Python install.
pip3 install -r requirements.txt

# After configuring project, you can run using the following.
python3 src/main.py -c ./settings.json
```

**NOTE**: Docker Compose files are included for easy deployment!

## Command Line Options
The following command line options are supported.

| Args | Default | Description |
| --------- | ------- | ----------- |
| `-c --cfg` | `./settings.json`  | The path to the config file using the JSON syntax. |
| `-l --list` | - | If set, will print the value of all settings from the config file and exit program. |

## Configuration
All configuration is set inside of a config file using JSON. The default settings file is searched at `./settings.json`. This can be changed using the command line options mentioned above.

Feel free to copy [`settings.ex.json`](./settings.ex.json) to `./settings.json` to make things easier!

Here is a list of all supported settings.

| Name | Type | Default | Description |
| ---- | ---- | ------- | -----------
| `debug` | Debug Object | `{}` | The debug object. |
| `general` | General Object | `{}` | The general object. |
| `bot` | Bot Object | `{}` | The Discord bot object. |
| `alert` | Alert Object | `{}` | The alert object. |

### Debug Object
Here are settings within the debug object.

| Name | Type | Default | Description |
| ---- | ---- | ------- | -----------
| verbose | int | `1` | The debug/verbose level. |
| log_to_file | boolean | `false` | Whether to log to a file or not. |
| log_dir | string | `./logs` | If logging is enabled, will log files to this directory. |

### General Object
Here are settings within the general object.

| Name | Type | Default | Description |
| ---- | ---- | ------- | -----------
| save_locally | boolean | `true` | If enabled, will save the config file locally in a generalized format. |

### Bot Object
Here are settings within the bot object.

| Name | Type | Default | Description |
| ---- | ---- | ------- | -----------
| token | string | `NULL` | The Discord bot token to use. |
| channel_id | string | `NULL` | The channel ID to post alarms to. |
| user_id | string | `NULL` | The user ID that can acknowledge alarms. |
| first_emoji | string | `⏰` | If set, the bot will automatically react with this emoji after submitting the message (just makes it easier for the user). |

### Alert Object
Here are settings within the alert object.

| Name | Type | Default | Description |
| ---- | ---- | ------- | -----------
| timezone | string | `"America/Los_Angeles"` | The timezone to use when scheduling. |
| snooze_time | int | `1800` | The snooze time in seconds. |
| times | Array<string> | `[]` | An array of times to schedule using the 24-hour format (e.g. `["08:00", "10:00", "23:30"]`). |
| max_snoozes | int | `10` | The maximum amount of snooze messages per alarm. |
| alert_msg | string | `"{m} Timer up {n}!!!"` | The alarm message. |
| alert_msg_snooze | string | `"{m} Snoozed {min} minutes, {n}. Will alert again in {sec} seconds."` | The alarm snooze message. |
| alert_msg_ack | string | `"{m} Alert acknowledged, {n}!"` | The alarm acknowledge message. |
| alert_msg_max_snoozes | string | `"Max snoozes reached ({max_snoozes}). Alert dismissed for {n}."` | The alarm max snoozes message. |


## Credits
* [Christian Deacon](https://github.com/gamemann)