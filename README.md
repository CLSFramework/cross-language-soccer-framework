# Cross Language Soccer Framework

Cross Language Soccer Framework is a new approach to enhance the flexibility and interoperability of RoboCup Soccer Simulation 2D (SS2D). The Soccer Simulation Proxy is an extended version of the Helios base that can send decision-making information to the PlayMaker Server. It can receive high-level actions from the PlayMaker Server and send them to RoboCup Soccer Simulation Server and/or SoccerWindow2.
On the other hand, the PlayMaker Server receives information from the client and selects the appropriate actions to be sent back to the client. We have implemented some sample servers in C\#, Python, and JavaScript, but it can also be implemented in other languages to make use of their features.

![mainflow](https://github.com/Cyrus2D/CrossLanguageSoccerFramework/assets/25696836/3ad98656-61a2-4830-8c65-71494b1dee0e)

## Definitions

### [RoboCup](https://www.robocup.org/)

RoboCup is an international robotics competition that focuses on promoting research and development in the field of autonomous robots. The competition aims to advance the state of the art in robotics and artificial intelligence by challenging teams to develop robots capable of playing soccer, rescue, and other tasks against other teams in a real-world or simulated environments.

### [RoboCup Soccer Simulation 2D](https://rcsoccersim.github.io/)

RoboCup Soccer Simulation 2D is a league in the RoboCup competition that focuses on developing autonomous soccer-playing agents. The goal of the league is to develop intelligent agents that can play soccer in a simulated environment. The agents must be able to perceive the game state, make decisions based on that information, and execute actions to play the game effectively.

![Screenshot 2024-01-06 135930](https://github.com/Cyrus2D/CrossLanguageSoccerFramework/assets/25696836/0202c371-57ee-42e3-89d9-69d7e429f220)

### [RoboCup Soccer Simulation Server](https://github.com/rcsoccersim/rcssserver)

The RCSSServer is a soccer server for the RoboCup Soccer Simulation 2D. It is a program that simulates a soccer game between two teams of eleven players and one coach each. The server provides a complete simulation of the game, including the physics of the ball, the field, and the players, as well as the dynamics of the game, such as the rules, the referee, and the game clock.

### [RoboCup Soccer Simulator Monitor](https://github.com/rcsoccersim/rcssmonitor)

RoboCup Soccer Simulator Monitor (rcssmonitor) is used to view the simulation as it takes place by connecting to the RoboCup Soccer Simulator Server (rcssserver) or to view the playback of a simulation by loading game log files.

### [Helios Base Code](https://github.com/helios-base/helios-base)

The Helios Base Code is a framework for the RoboCup Soccer Simulation 2D. It is a collection of software components that provide a common infrastructure for developing soccer simulation 2D teams. The base code is designed to be easy to use and extend, and it provides a number of features that make it easier to develop teams.

### [gRPC](https://grpc.io/docs/what-is-grpc/)

gRPC is a high performance, open source, general-purpose RPC framework that puts mobile and HTTP/2 first. gRPC is based on the HTTP/2 standard, which is the next generation of HTTP. HTTP/2 is a binary protocol that is more efficient than HTTP/1.1, which is the current version of HTTP. HTTP/2 is also more secure than HTTP/1.1, because it uses TLS encryption by default.

### [Soccer Simulation Proxy](https://github.com/Cyrus2D/SoccerSimulationProxy)

We have modified the Helios base code to enhance its interaction capabilities with the gRPC server. Specifically, the base code now transmits detailed information about each game cycle to the server, which in response, sends back a series of potential actions. This bidirectional communication enables the PlayMaker Server to effectively process and make strategic decisions based on the incoming data.

To facilitate this enhanced functionality, the client is designed to serialize various data types—such as the WorldModel, FullState WorldModel, Server Parameters, Player Parameters, and Player Types—into gRPC messages during each game cycle. Conversely, it also deserializes incoming gRPC action messages back into Helios base actions.

These improvements ensure that the Helios base maintains its inherent efficiency and performance, while now being able to seamlessly interact with a diverse array of programming languages through gRPC. This modification not only preserves the robustness of the original system but also expands its utility and applicability in multi-language research environments.

### Playmaker Server

The Playmaker Server acts as the decision-making hub within our framework, receiving and processing messages from the Soccer Simulation Proxy. Based on the detailed information conveyed in these messages, it evaluates the current game state and strategically generates corresponding actions to be executed in the simulation.

To demonstrate the versatility and language-agnostic design of our framework, we have developed initial implementations of the Playmaker Server in three different programming languages: C#, Python, and JavaScript. These examples serve to showcase the server’s capability to operate effectively across diverse programming environments. Looking ahead, we aim to extend this functionality by developing additional server implementations in other languages, further broadening the framework's accessibility and appeal to a global research community.

- [PlaymakerServer-CSharp](https://github.com/Cyrus2D/PlaymakerServer-CSharp)
- [PlaymakerServer-Python](https://github.com/Cyrus2D/PlaymakerServer-Python)
- [PlaymakerServer-NodeJs](https://github.com/Cyrus2D/PlaymakerServer-NodeJs)

![Screenshot 2024-04-07 012206](https://github.com/Cyrus2D/CrossLanguageSoccerFramework/assets/25696836/3f67fcfe-0fe6-4957-8df5-d728886f6f01)

![detailflow](https://github.com/Cyrus2D/CrossLanguageSoccerFramework/assets/25696836/745f3760-96f2-434f-a54b-20eca2dd7433)


### Why not develop a base code for each language?

Developing a base code for each language is a time-consuming task. It requires a lot of effort to develop a base code for each language. The RCSSServer send noisy observation to players and receives low level actions from player such as Dash, Turn, Kick. So, a sample base code should process the received information, denoise information, create a model, make decision, convert high level decision like BodySmartKick, BodyGoToPoint and ... to low level actions and send them to RCSSServer. Therefor, developing a base code for each language is a time-consuming task, also some of the languages are not high performance same as C++ and can not do all of the tasks in a cycle (0.1 second). By using this framework, the SS2D-gRPC-Base denoise information, creates models, sends them to SS2D-gRPC-Server and receives actions from SS2D-gRPC-Server and send them to RCSSServer. So, the SS2D-gRPC-Server can be developed in any language supported by gRPC and its reponsibility is just making decision and sending actions to SS2D-gRPC-Base.

## How To Use The Framework?

To run a normal soccer simulation 2D game without using the proxy, you need to run the Soccer Simulation Server (RCSSServer) and the Soccer Simulator Monitor (RCSSMonitor). The Soccer Simulation Server will host the game, and the Soccer Simulator Monitor will display the game. Also, you need to run two teams to play the game. Each team should have a coach and eleven players.

To run a game by using the framework, you need to run the Soccer Simulation Server to host a game, the Soccer Simulator Monitor, Soccer Simulation Proxy, and a Playmaker Server. We provide some different solution to build, install, and run these components on Linux(Ubuntu) [Build From Source, AppImage, Docker] and Windows[WSL, Docker]. Also, there are some solutions that you can run some of the components together.

# Build, install, and run each component separately

This solution is the best for developers who want to modify the source code of each component. So, you have to build and install RoboCup Soccer Simulation Server, Soccer Simulation Proxy, and Playmaker Server separately.

## Soccer Simulation Server

### Build from source, install, and run (Linux, WSL)

To install the Soccer Simulation Server, you can follow the instructions provided in the [repository](https://github.com/rcsoccersim/rcssserver).

```bash
sudo apt update
sudo apt install build-essential automake autoconf libtool flex bison libboost-all-dev cmake git
git clone git@github.com:rcsoccersim/rcssserver.git
cd rcssserver
mkdir build
cd build
cmake ..
make
sudo make install
```

To run the Soccer Simulation Server, you can use the following command:

```bash
rcssserver
```

Be aware that the log files of the Soccer Simulation Server will be saved in the current directory.

Also, you can change configuration of the Soccer Simulation Server from "~/.rcssserver/server.conf" file.
For example, you can change the following parameters:

- server::synch_mode, to change the mode of the server to synchronous or asynchronous. If the synch_mode is true, the server wait to receive actions from all agents before going to the next cycle.

- server::auto_mode, to change the mode of the server to auto or manual. If the auto_mode is true, the server will start the game automatically.

- server::fullstate_l, to change the fullstate mode of the server. If the fullstate_l is true, the server will send the fullstate information (without noise) to the agents.

### Use AppImage (Linux, WSL)

You can download the AppImage of the Soccer Simulation Server from the #### and run it.

```bash
```

- Changing configuration is same as the build from source.

### Use Docker (Linux, WSL, Windows)

## Soccer Simulator Monitor

### Build from source, install, and run (Linux, WSL)

```bash
sudo apt update
sudo apt install build-essential qt5-default libfontconfig1-dev libaudio-dev libxt-dev libglib2.0-dev libxi-dev libxrender-dev git
git clone git@github.com:rcsoccersim/rcssmonitor.git
cd rcssmonitor
mkdir build
cd build
cmake ..
make
sudo make install
```

To run the Soccer Simulator Monitor, you can use the following command:

```bash
rcssmonitor
```

- if you installed the monitor on WSL, you need to install an X server on Windows.

### Use AppImage (Linux, WSL)

You can download the AppImage of the Soccer Simulator Monitor from the #### and run it.

```bash
```

## Soccer Window 2

The [Soccer Window 2](https://github.com/helios-base/soccerwindow2) is a monitor for Soccer Simulation Server, but it is more power full than the Soccer Simulator Monitor. You can use it to monitor the game and also to control the game, also the agents can connect to the Soccer Window 2 to show logs and debug information.

### Build from source, install, and run (Linux, WSL)

Follow the instructions provided in the [repository](https://github.com/helios-base/soccerwindow2).

### Use AppImage (Linux, WSL)

You can download the AppImage of the Soccer Window 2 from the #### and run it.

```bash
```

## Soccer Simulation Proxy

### Build from source, install, and run (Linux, WSL)

To build the soccer simulation proxy, you need to install the following dependencies:

#### LibRCSC

```bash
git clone git@github.com:helios-base/librcsc.git
cd librcsc
git checkout 19175f339dcb5c3f61b56a8c1bff5345109f22ef
mkdir build
cd build
cmake ..
make
make install
```

#### gRPC - follow the instructions provided in the [repository](https://grpc.io/docs/languages/cpp/quickstart/)

```bash
export MY_INSTALL_DIR=$HOME/.local
mkdir -p $MY_INSTALL_DIR
export PATH="$MY_INSTALL_DIR/bin:$PATH"
sudo apt install -y build-essential autoconf libtool pkg-config
git clone --recurse-submodules -b v1.62.0 --depth 1 --shallow-submodules https://github.com/grpc/grpc
cd grpc/
mkdir -p cmake/build
pushd cmake/build
cmake -DgRPC_INSTALL=ON       -DgRPC_BUILD_TESTS=OFF       -DCMAKE_INSTALL_PREFIX=$MY_INSTALL_DIR       ../..
make -j 4
make install
```

then, add the following lines at the end of $HOME/.bashrc

```bash
export MY_INSTALL_DIR=$HOME/.local
export PATH="$MY_INSTALL_DIR/bin:$PATH"
```

then, run the following command

```bash
source $HOME/.bashrc
```

To test grpc, go to grpc directory (in this example it is in $HOME/grpc) and run the following commands:

```bash
cd examples/cpp/helloworld
mkdir -p cmake/build
cd cmake/build/
cmake -DCMAKE_PREFIX_PATH=$MY_INSTALL_DIR ../..
make
run ./greeter_server in one tab
run ./greeter_client in another tab
```

#### SoccerSimulationProxy

```bash
git clone git@github.com:Cyrus2D/SoccerSimulationProxy.git
cd SoccerSimulationProxy
mkdir build
cd build
cmake ..
make
```

Troubleshooting

If you saw an error about the different version of GRpc
You should delete src/grpc/service.pb.cc and src/grpc/service.pb.h
Then, generate them again by going to the base root directory and

```bash
cd grpc/proto
protoc --proto_path=. --cpp_out=../../src/grpc/ --grpc_out=../../src/grpc/ --plugin=protoc-gen-grpc=$HOME/.local/bin/grpc_cpp_plugin service.proto
```

To run the Soccer Simulation Proxy, you can use the following command: (You should run the Soccer Simulation Server and a PlayMaker Server before running the Soccer Simulation Proxy)

```bash
cd build/bin
./start.sh
```

To run the Soccer Simulation Proxy in debug mode, you can use the following command:

```bash
cd build/bin
./start-debug.sh
```

To run the Soccer Simulation Proxy with different configuration, you can pass the following parameters to start.sh or start-debug.sh:

- -h, --host HOST              >>> specifies server host (default: localhost)"
- -p, --port PORT              >>> specifies server port (default: 6000)"
- -P  --coach-port PORT        >>> specifies server port for online coach (default: 6002)"
- -t, --teamname TEAMNAME      >>> specifies team name"
- -n, --number NUMBER          >>> specifies the number of players"
- -u, --unum UNUM              >>> specifies the uniform number of players"
- -C, --without-coach          >>> specifies not to run the coach"
- -f, --formation DIR          >>> specifies the formation directory"
- --team-graphic FILE          >>> specifies the team graphic xpm file"
- --offline-logging            >>> writes offline client log (default: off)"
- --offline-client-mode        >>> starts as an offline client (default: off)"
- --debug                      >>> writes debug log (default: off)"
- --debug_DEBUG_CATEGORY       >>> writes DEBUG_CATEGORY to debug log"
- --debug-start-time TIME      >>> the start time for recording debug log (default: -1)"
- --debug-end-time TIME        >>> the end time for recording debug log (default: 99999999)"
- --debug-server-connect       >>> connects to the debug server (default: off)"
- --debug-server-host HOST     >>> specifies debug server host (default: localhost)"
- --debug-server-port PORT     >>> specifies debug server port (default: 6032)"
- --debug-server-logging       >>> writes debug server log (default: off)"
- --log-dir DIRECTORY          >>> specifies debug log directory (default: /tmp)"
- --debug-log-ext EXTENSION    >>> specifies debug log file extension (default: .log)"
- --fullstate FULLSTATE_TYPE   >>> specifies fullstate model handling"
- --g-ip GRPC IP               >>> specifies grpc IP (default: localhost)"
- --g-port GRPC PORT           >>> specifies grpc port (default: 50051)"
- --diff-g-port                >>> specifies different grpc port for each player (default: false)"
- --gp20                       >>> add 20 to GRPC Port if team run on right side (default: false)"

### Use AppImage (Linux, WSL)

You can download the AppImage of the Soccer Simulation Proxy from the #### and run it.

```bash
```

### Use Docker (Linux, WSL, Windows)

## Playmaker Server (PYTHON)


## Related Repositories

- [Soccer Simulation Server](https://github.com/rcsoccersim/rcssserver)
- [SoccerSimulationProxy](https://github.com/Cyrus2D/SoccerSimulationProxy)
- [PlaymakerServer-CSharp](https://github.com/Cyrus2D/PlaymakerServer-CSharp)
- [PlaymakerServer-Python](https://github.com/Cyrus2D/PlaymakerServer-Python)
- [PlaymakerServer-NodeJs](https://github.com/Cyrus2D/PlaymakerServer-NodeJs)
