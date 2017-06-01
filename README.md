# tmux-mem-cpu-load

## CPU, RAM, and load monitor for use with tmux


![](https://travis-ci.org/dean-wong/tmux-mem-cpu-load.svg)

## 说明

在tmux上显示系统信息，[powerline-status](https://pypi.python.org/pypi/powerline-status/)的效率较低，[thewtex](http://github.com/thewtex/tmux-mem-cpu-load)是一个更好的方案，但原项目中没有显示CPU温度，本工程在thewtex基础上增加了CPU温度显示。

### Sample
```lisp
set -g status-left-length 20
set -g status-left '#[fg=#fff6da]#S '
set -g status-left-attr bold
set -g status-right-length 60
set -g status-right '#(tmux-mem-cpu-load -i 2 -q -c -a 0) %R'
set -g status-right-attr default
```

#### macOS

![macOS](https://ws4.sinaimg.cn/large/006tKfTcgy1fg5t0km08xj30iy08owel.jpg)

#### Linux

![Raspberry Pi 3](https://ws1.sinaimg.cn/large/006tKfTcgy1fg5t0o9ki4j30iy08ot8u.jpg)

## Description

A simple, lightweight program provided for system monitoring in the *status* line of **tmux**.

The memory monitor displays the used and available memory.

The CPU usage monitor outputs **CPU temperature** and a percent CPU usage over all processors. It also
displays a textual bar graph of the current percent usage.

The system load average is also displayed.

Example output:
```
  2885/7987MB 57.2°C [|||||     ]  51.2% 2.11 2.35 2.44

   ^    ^       ^         ^          ^     ^    ^    ^
   |    |       |         |          |     |    |    |
   1    2       3         4          5     6    7    8
```

1. Currently used memory.
2. Available memory.
3. **CPU temperature.**
4. CPU usage bar graph.
5. CPU usage percentage.
6. Load average for the past minute.
7. Load average for the past 5 minutes.
8. Load average for the past 15 minutes.

For `terminals with 256 color support`, graded colors can be displayed by passing the **--colors** flag.

## Installation


### Dependencies


Currently, Linux, Mac OSX, FreeBSD, OpenBSD, and NetBSD are supported.

#### Building


* >= CMake_ -2.6
* C++ compiler with C++11 support (e.g. gcc/g++ >= 4.6)

### Download


There are links to the source code at the [project homepage](http://github.com/dean-wong/tmux-mem-cpu-load)



### Build

```shell
  cd <source dir>
  mkdir -p build && cd build
  cmake ..
  make
```

### Install

```shell
  su -
  make install
  logout
```

## Configuring tmux_

Edit ``$HOME/.tmux.conf`` to display the program's output in *status-left* or
*status-right*.  For example:

```lisp
  set -g status-interval 2
  set -g status-left "#S #[fg=green,bg=black]#(tmux-mem-cpu-load --colors --interval 2)#[default]"
  set -g status-left-length 60

```

If you installed using tpm, you must specify the full path to the
``tmux-mem-cpu-load`` script, like below:
```lisp
  set -g status-right "#[fg=green]#($TMUX_PLUGIN_MANAGER_PATH/tmux-mem-cpu-load/tmux-mem-cpu-load --colors --powerline-right --interval 2)#[default]"
```

Note that the *interval* argument to `tmux-mem-cpu-load` should be the same number
of seconds that *status-interval* is set at.

Another optional argument is the number of bars in the bar graph, which
defaults to 10.  This can, for instance, be set to the number of cores in a
multi-core system.

The *colors* option will add graded colors for each of the measures.

The full usage:

```shell
  Usage: tmux-mem-cpu-load [OPTIONS]

  Available options:
  -h, --help
           Prints this help message
  -c, --colors
          Use tmux colors in output
  -p, --powerline-left
	  Use powerline left symbols throughout the output, enables --colors
  -q, --powerline-right
	  Use powerline right symbols throughout the output, enables --colors
  -i <value>, --interval <value>
          Set tmux status refresh interval in seconds. Default: 1 second
  -g <value>, --graph-lines <value>
          Set how many lines should be drawn in a graph. Default: 10
  -m <value>, --mem-mode <value>
        Set memory display mode. 0: Default, 1: Free memory, 2: Usage percent.
  -t <value>, --cpu-mode <value>
        Set cpu % display mode. 0: Default max 100%, 1: Max 100% * number of threads.
  -a <value>, --averages-count <value>
        Set how many load-averages should be drawn. Default: 3
```


## Authors

Matt McCormick (thewtex) <matt@mmmccormick.com>

Contributions from:

* cousine <iam@cousine.me>
* Jasper Lievisse Adriaanse <jasper@humppa.nl>
* Justin Crawford <justinc@pci-online.net>
* krieiter <krieiter@gmail.com>
* Mark Palmeri <mlp6@duke.edu>
* `Pawel 'l0ner' Soltys`_ <pwslts@gmail.com>
* Travil Heller <trav.heller@gmail.com>
* Tony Narlock <tony@git-pull.com>
* Compilenix <Compilenix@compilenix.org>
* jodavies <jodavies1010@gmail.com>
* `@nhdaly`_ (Nathan Daly) <nhdaly@gmail.com>


[tmux](http://tmux.sourceforge.net/)
[CMake](http://www.cmake.org)
[terminals with 256 color support]( http://misc.flogisoft.com/bash/tip_colors_and_formatting#terminals_compatibility)
[Pawel 'l0ner' Soltys](http://l0ner.github.io/)
[nhdaly](http://github.com/nhdaly)

