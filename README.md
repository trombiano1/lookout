# Lookout: Command watcher w/ Slack
![example image](https://i.stack.imgur.com/fIh5J.png)
## About
Lookout is a simple yet powerful CLI app that sends a **slack notification** when your program

1. completes successfully,
2. terminates with an error,
3. exceeds predefined time without any output, or
4. outputs predefined regex match.

Usage is very simple as well; say you wanted to run:
```sh
$ python really_heavy_program.py arg1 arg2
```
With lookout, just do:
```sh
$ lookout python really_heavy_program.py arg1 arg2
```

#### Example usages:
- Waiting for installation (or worse yet, conda's infamous `Solving environment: \`)
  ```sh
  $ lookout --regex "\(\[y\]\/n\)\?" conda install opencv
  ```
  This matches conda's prompt `([y]/n)?` and sends a notification when it's asking for user input.
- Running very long machine learning programs on background servers
  ```sh
  $ nohup lookout python train.py
  ```
  This will run `python train.py` in the background even with the terminal closed, and you will get a notification when it's done.

## Installation
```sh
$ pip install lookout-python
```
When you run `lookout` for the first time, you will be asked to log in to your Slack application via browser.

After authentication, you will be displayed a code that you need to copy and paste into your terminal window.

## Options
- Set timeout threshold
  ```
  --hangthreshold 120
  ```
  This will set `hangthreshold` to 120 seconds and will send a `Process may be hanging` alert after 120 seconds. This value will be saved for next time.

- Using regex
  ```sh
  --regex "expression"
  ```
  This will send an alert when the command output matches given regex. Make sure to escape symbols with backslash. Double quotes are only required on some cases (to escape `sh`).

- Change slack channel
  ```sh
  $ lookout --change
  ```
  Run this in order to update or change your Slack channel.

- Reset
  ```
  $ lookout --reset
  ```
  This will reset to factory settings.

## Limitations
- Color of output may be stripped. This is because some programs strip color from output when it detects that it is outputting to anything else than an actual terminal, and this program uses pipe to parse data.

## Changelog
#### 1.0.0 (2023/02/19)
Initial release.