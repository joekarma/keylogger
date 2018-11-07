# Mac OS X Keylogger

This repository holds the code for a simple and easy to use keylogger for Mac OS X. It is not meant to be malicious, and is written as a proof of concept, though it can be adapted for personal analytics such as described by [Stephen Wolfram](http://blog.stephenwolfram.com/2012/03/the-personal-analytics-of-my-life/). There is not a lot of information on keyloggers or implementing them on Mac OS X, and most of the ones I've seen do not work as indicated. This project aims to be a simple implementation on how it can be accomplished on OS X.

> Note: This keylogger is currently unable to capture secure input such as passwords. See issue #3 for more information.

## Usage

Start by cloning the repository and running the proper make commands, shown below. By default, the application installs to `/usr/local/bin/keylogger`, which can easily be changed in the [`Makefile`](https://github.com/joekarma/keylogger/blob/master/Makefile). `make install` may require root access.

```bash
$ git clone https://github.com/joekarma/keylogger && cd keylogger
$ make && make install
```

The application by default logs to `/var/log/keystroke-<timestamp>.log`, which may require root access depending on your system's permissions. You can change this in `keylogger.c` if necessary. The inclusion of the timestamp in the log file name is so that log files can more easily be backed up, to the cloud, for example.

```bash
$ keylogger
Logging to: /var/log/keystroke-<timestamp>.log
```

If you'd like the application to run on startup, run the `startup` make target:

```bash
$ sudo make startup
```

## Format of the log file

The log file stores each keystroke on its own line, with an epoch timestamp with seconds level granularity - eventually I might change this to milliseconds level granularity, but implementation for that is [slightly more complicated](https://stackoverflow.com/questions/3756323/how-to-get-the-current-time-in-milliseconds-from-c-in-linux). The log file format is perhaps better explained with an example, shown below.

```
 1541558124 [logging started]
1541558126 [left-shift]
1541558126 t
1541558126 [left-shift]
1541558126 h
1541558126 e
1541558126  
1541558126 l
1541558126 o
1541558126 g
1541558126  
1541558126 f
1541558127 i
1541558127 l
1541558127 e
1541558127  
1541558127 f
1541558127 o
1541558128 r
1541558128 m
1541558128 a
1541558128 t
1541558128  
1541558128 i
1541558128 s
1541558128  
1541558128 p
1541558128 e
1541558128 r
1541558128 h
1541558128 a
1541558128 p
1541558128 s
1541558128  
1541558128 b
1541558128 e
1541558128 t
1541558128 t
1541558128 e
1541558128 r
1541558128  
1541558129 d
1541558129 e
1541558129 [del]
1541558129 e
1541558129 [del]
1541558129 [del]
1541558129 e
1541558129 x
1541558129 p
1541558129 l
1541558129 a
1541558129 i
1541558129 n
1541558129 e
1541558129 d
1541558133  
1541558133 w
1541558133 i
1541558133 t
1541558133 h
1541558133  
1541558133 a
1541558133 n
1541558133  
1541558133 e
1541558133 x
1541558133 a
1541558133 m
1541558133 p
1541558133 l
1541558133 e
1541558133 ,
1541558133  
1541558133 s
1541558133 h
1541558133 o
1541558133 w
1541558133 n
1541558133  
1541558133 b
1541558133 e
1541558133 l
1541558133 o
1541558133 w
1541558133 [left-shift]
1541558133 [left-shift]
1541558133 .
1541558133 [left-ctrl]
1541558133 k
1541558133 [left-ctrl]
1541558133 [left-ctrl]
1541558133 c
```

In the future, I might also add instrumentation for keyup events, so that it's more clear, for example, what letters are capitalized. It might be interesting to explore what information can be derived from these timestamps - it's possible that they could serve as a fingerprint of sorts, which has all sorts of implications for privacy.

## Uninstallation

You can completely remove the application from your system (including the startup daemon) by running the following command (logs will not be deleted):

```bash
$ sudo make uninstall
```

## Contributing

Feel free to fork the project and submit a pull request with your changes!
