Social P2P App Platform
---

Many web applications can be modelled as some User Interface which allows a user, or group of users, to update some persistent state (typically a database of some kind). Databases can be considered the latest state from a [stream of events](https://www.martinfowler.com/eaaDev/EventSourcing.html).

This architecture can be fit well onto a peer to peer storage pattern. Some User Interface generates events, these events update the local state. In addition, these events can be sent to other parties over a peer to peer networks.

Databases that model this paradigm exist. Examples include [orbit-db](https://github.com/orbitdb/orbit-db), [gunDB](https://gun.eco/), and so on.

[SSB](https://scuttlebutt.nz) is a peer to peer social network. It uses public keys as identities. It also includes an encrypted messaging function.

Our mission is to combine these approaches to create a p2p app platform.

## Platform

Our vision is to create an SDK and application distribution platform which is based on a decentralised social network. An application consists of some user interface, some business logic to update state, and a specification for what state updates look like. The platform layer we are building will handle the encryption, storage, and distribution of messages. It will also expose the user's peer connections.

### Tic tac toe

An example flow between two users:

* Alice sends Bob an invitation to play tic tac toe
	* The invitation includes a copy of the app
* Bob accepts the invitation
* Alice plays the first move
	* Alice's local state is updated
	* This move is sent to Bob via the underlying platform
	* Bob's state is updated after the move has been received
* Bob makes the next move
	* Bob's local state is updated
	* The move is sent to Alice via the platform
	* Alice's state is updated
* This repeats until the game is finished

### Shared Todo

Todo apps are the quintessential example in recent times. The same architecture above can work for a shared todo app. Each user has a UI which shows them the current state. Each user can take actions in the UI which are sent to the other user(s).

The application developer need only build the UI and business logic to deal with incoming events. 
