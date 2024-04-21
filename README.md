# Cross Language Soccer Framework

We have introduced a new approach called Cross Language Soccer Framework to enhance the flexibility and interoperability of RoboCup Soccer Simulation 2D (SS2D). The Cross Language Soccer approach consists of two components: Soccer Simulation Proxy and PlayMaker Server.
The Soccer Simulation Proxy is an extended version of the Helios base that can send decision-making information to the PlayMaker Server. It can receive high-level actions from the PlayMaker Server and send them to RoboCup Soccer Simulation Server and/or SoccerWindow2.
On the other hand, the PlayMaker Server receives information from the client and selects the appropriate actions to be sent back to the client. We have implemented some sample servers in C\#, Python, and JavaScript, but it can also be implemented in other languages to make use of their features.

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

## How To Use The Framework?

To run the framework, you need to run the Soccer Simulation Server, Soccer Simulation Proxy, and Playmaker Server. This framework provide some different solution to build, install, and run these three components.

### Build, install, and run each component separately

This solution is the best for developers who want to modify the source code of each component. So, you have to build and install RoboCup Soccer Simulation Server, Soccer Simulation Proxy, and Playmaker Server separately.

#### Soccer Simulation Server

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

## Related Repositories

- [Soccer Simulation Server](https://github.com/rcsoccersim/rcssserver)
- [SoccerSimulationProxy](https://github.com/Cyrus2D/SoccerSimulationProxy)
- [PlaymakerServer-CSharp](https://github.com/Cyrus2D/PlaymakerServer-CSharp)
- [PlaymakerServer-Python](https://github.com/Cyrus2D/PlaymakerServer-Python)
- [PlaymakerServer-NodeJs](https://github.com/Cyrus2D/PlaymakerServer-NodeJs)
