# Mac OS X Keylogger

This repository holds the code for a simple and easy to use keylogger for Mac OS X. It is not meant to be malicious, and is written as a proof of concept, though it can be adapted for personal analytics such as described by [Stephen Wolfram](http://blog.stephenwolfram.com/2012/03/the-personal-analytics-of-my-life/). There is not a lot of information on keyloggers or implementing them on Mac OS X, and most of the ones I've seen do not work as indicated. This project aims to be a simple implementation on how it can be accomplished on OS X.

> Note: This keylogger is currently unable to capture secure input such as passwords. See issue #3 for more information.

## Usage

Start by cloning the repository and running the proper make commands, shown below. By default, the application installs to `/usr/local/bin/keylogger`, which can easily be changed in the [`Makefile`](https://github.com/joekarma/keylogger/blob/master/Makefile). `make install` may require root access.

```bash
$ git clone https://github.com/joekarma/keylogger && cd keylogger
$ make && make install
```

The application by default logs to `/var/log/keystroke-<timestamp>.log`, which may require root access depending on your system's permissions. You can change this in `keylogger.c if necessary. Logs are split by timestamp of keylogger start so that they can more easily be backed up.

```bash
$ keylogger
Logging to: /var/log/keystroke-<timestamp>.log
```

If you'd like the application to run on startup, run the `startup` make target:

```bash
$ sudo make startup
```

## Uninstallation

You can completely remove the application from your system (including the startup daemon) by running the following command (logs will not be deleted):

```bash
$ sudo make uninstall
```

## Contributing

Feel free to fork the project and submit a pull request with your changes!
