# Interactive Program Execution Environment 1.0

**Interactive Program Execution Environment 1.0** is a CLI tool designed to automatically execute programs in response to changes in local files. It monitors directories for changes, and when a file change is detected, the configured external program (with optional arguments) gets executed. 

## Features

- **Directory Monitoring**: Monitors specified directories for file changes.
- **Automatic Execution**: Executes a configured external program automatically when a file change is detected.
- **Interactive Mode**: Allows users to interactively start, configure, and manage monitored programs.
- **Customizable Settings**: Configurable via a JSON settings file (`interactive.json`), allowing users to specify directories to monitor and the program to execute.
- **Latency Handling**: Configurable delay between file changes and command execution to avoid triggering too many executions in a short time.

## Installation

### Prerequisites

- Python 3.9 or higher
- Required Python libraries:
  - `setproctitle` – For setting the process title.
  - `watchdog` – For monitoring file changes.
  - `argparse` – For command-line argument parsing.
  - `readline` – For handling command history in interactive mode.

To install the required libraries, use `pip`:

```bash
pip install setproctitle watchdog
```

### Linux

1. Place program file `cast` (without Python extension `py`) under `~/local/bin` (Linux).

2. In the hidden file `.bashrc` located in the user's home directory, add the following,

   `export PATH=$HOME/.local/bin:$PATH`

   if this search path for executable scripts is not yet known.

## Usage

**1. Initial Setup**

Before using the tool, initialize a configuration file (`interactive.json`) with the `init` subcommand:

```
python interactive.py init
```

or if stored in the local / system-wide bin folder (without file extension):

```bash
interactive init
```

This will create a configuration file with the following structure:

```
{
	"monitored_dirs": ["./"],
	"program": "echo",
	"args": "Hello, World!"
}
```

You can edit this file to specify which directories you want to monitor and which program to run when changes occur.

**2. Start the Interactive Program**

To start the interactive environment, run the following command:

```
python interactive.py
```

This will start the program and allow you to interactively manage the monitored directories and the program to execute.

### Commands

Once in the interactive environment, you can use the following commands:

- `start <command>`: Set the program to execute and start monitoring directories for changes.
- `apply <arguments>`: Update the arguments for the program and execute it immediately.
- `kill`: Terminate any running processes.
- `restart`: Restart the monitoring and execution of the program.
- `quit` or `exit`: Exit the interactive environment.

Example of starting the program:

```
> start echo Hello, World!
```

The program will start monitoring the specified directories, and whenever a file is changed, the `echo Hello, World!` command will be executed.

### Configuration File

The configuration file (`interactive.json`) allows users to specify the following:

- `monitored_dirs`: A list of directories to monitor for file changes.
- `program`: The external program to execute when a file change is detected.
- `args`: Arguments to pass to the external program.

Example:

```
{
  "monitored_dirs": ["./src", "./config"],
  "program": "python",
  "args": "process_data.py"
}
```

## How It Works

1. **File Monitoring**: The program monitors  changes in the directories specified in the configuration file. It  watches for file modifications, creations, moves, and deletions.
2. **Program Execution**: When a file change is detected, the tool waits for a brief period  (configurable latency) before executing the external program. This delay prevents executing the program multiple times for rapid changes.
3. **Interactive Mode**: Users can interactively manage the tool, change the program to execute, and monitor file changes in real time.

## License

This software is released into the **public domain** under the [Unlicense](http://unlicense.org/). You are free to use, modify, and distribute it as you wish.
