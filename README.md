# AdeptServer

Collection of [V+](https://en.wikipedia.org/wiki/Omron_Adept#Hardware_and_Software_History) programs for the Adept robot platform realizing a TCP server in the robot controller, intended to accept commands and execute predefined robot skills. 

The code in this repository is created with the primary purpose of running in tandem with the [`pyadept`](https://github.com/semeniuta/pyadept) library for flexible control of robot applications with [AsyncIO](https://docs.python.org/3/library/asyncio.html)-based logic. However, it can certainly be used in other cases beyond this architecture. 

## Code structure

Files with the `.V2` extension constitute V+ modules, each containing a number of programs. Every program ends with the form feed (`FF`) character (ASCII code 12), which serves as a delimiter when the module is parsed by the robot controller. The module ends with the substitute (`SUB`) character (ASCII code 26).

The present-state codebase is in the early development state. The most general-purpose V+ programs are collected in the `adeptserver` module. Other modules contain setup-specific programs and legacy code. 

## Launching the server

The guidelines in this section are based on the GUI elements of the Adept DeskTop programming software (tested with Adept SmartController CX and Adept Viper s850 robot). 

Click *Open Program* button on the *Program Manager* pane to open a V+ file. Note that several V+ modules have to be opened seperately (if they are selected at once, all V+ programs from will appear as belonging to the same module in the *Program Manager*). Load the `adeptserver.V2` module in this way.

Adept robot controller can run 28 concurrent tasks (identified in the range {0 ... 27}). To launch a V+ program, the latter has to be associated with a task. To to this, the selected program has to be dragged from the *Program Manager* to a free task in the *Task Manager*. Then, the *Execute Task* button on the *Task Manager* pane should be pressed while the target task is selected. To launch the server, perform these actions for the `server` program. 

The set of skills that the server is able to invoke comrises all V+ programs that have been loaded into the *Program Manager*. These include the programs from the `adeptserver` module, as well as any custom routines the system programmer creates. 

## References

Please refer to the following research [preprint](https://peerj.com/preprints/27552/) for more information about AdeptServer and `pyadept`:

 * Semeniuta O, Falkman P. 2019. Event-driven industrial robot control architecture for the Adept V+ platform. PeerJ Preprints 7:e27552v1 https://doi.org/10.7287/peerj.preprints.27552v1


