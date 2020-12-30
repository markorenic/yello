# yello
An online game for multiplayer pacman with voice control ability
Demo: https://youtu.be/01UEHb65p0M
https://cdn.discordapp.com/attachments/724007028410023948/724472471843110952/unknown.png
## Inspiration
With all of us cooped up in our homes, we’ve found new ways to connect with one another and future classmates, forging new friendships through Discord calls and online multiplayer games. We wanted to implement a game we all loved, with a competitive and novel twist: voice activation! Not only is our game a fantastic community builder, it challenges the brain and strengthens reading skills while being an accessible way to play.

## What it does
Yello takes inspiration from the classic Pacman and takes it to a new level with its online multiplayer approach. One player controls the Yello character, while four others control the ghosts—to up the ante, each player is voice-controlled by a set of rapidly changing commands.

The purpose of our novel navigation system is threefold: to provide an extra challenge to the player, to build reading skills in younger players, and to train the player’s brain to be quickly adaptive to new situations. With an NLP algorithm, we processed several sets of navigation voice commands: colours, directions, animals, and other common nouns. These are randomized periodically as the game progresses.

## How we built it
Yello’s client end is built in p5.js, making use of the Canvas element. The voice input uses the SoundClassifier from ml5.js, which we trained using Google’s TeachableMachine.

The game is implemented using websockets. The server is a multi-threaded Golang websockets server, making use of gorilla-WebSocket. Each client is assigned two threads: one for listening to the client and the other for writing to the information about the client. Other threads handle things like the game queue and game instances and communicate with the base threads of a client through client-specific channels. The server is set up to scale with any number of players.

The game instances are run such that each tile is simply an 8-bit integer. All collisions and inter-entity interactions are handled through bitmasks, making for an elegant game management system that is both super fast and easy to comprehend.


## Challenges we ran into
We initially attempted to implement the front-end using React and Redux. However, it was practically impossible to draw on canvases, and react was too slow for the intended task. As such, we had to quickly adapt to a simpler html/css/Processing.js model, which we found much easier to work with. 

Establishing communication between the JavaScript frontend and the Golang backend using web sockets proved to be challenging to implement robustly. We initially tried to use sockets.io, but after hours of work, we decided to just use WebSockets on the frontend without any 3rd party libraries. It has proven to be much more robust for our purposes.

## Accomplishments that we're proud of
- The effective and rapid switchover of the entire front-end tech stack
- A robust and scalable server that accounts for any number of messages and associated functions at compile-time. This is done through a simple and yet effective protocol that we wrote ourselves, which both the client and the server adhere to.


## What we learned
- Effective teamwork and collaboration! We sat in a call for almost 30 hours straight, making sure to communicate and reminding each other to git push and pull.
- Working in the Processing.js framework

## What's next for Yello
Yello will find its place in the io community of games. And it can be expanded with AI integration with a simple pathfinding algorithm for ghosts.
