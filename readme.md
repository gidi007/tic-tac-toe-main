Tic Tac Toe - Multiplayer Node.js Game

Welcome to the Tic Tac Toe Multiplayer Game, a classic game experience built with Node.js and powered by WebSocket communication for real-time, multiplayer gameplay! Join in at https://ttt.jakesgordon.com to play. You’ll either be matched with another player or, if preferred, you can test it solo by opening two separate browsers or devices.

Note: Game hosting may vary, so the availability of the online version is not guaranteed.


Getting Started
Easily launch the game by running the commands below in your terminal:

bash
Copy code
npm run dev        # Runs both client and server
npm run dev:client # Runs the client only
npm run dev:server # Runs the server only
npm run test       # Executes server unit tests
npm run lint       # Runs ESLint
npm run build      # Builds production assets


Project Structure


The game is designed with simplicity in mind using key modern web tools and languages:

Vite for the development server
TypeScript for type safety
HTML and CSS – no complex frameworks are required!
Directory Overview
plaintext
Copy code
index.html          - Core HTML structure
public              - Static assets
src
 ├── interface.ts   - Shared types for client and server
 ├── server.ts      - WebSocket server logic
 ├── client.ts      - WebSocket client logic
 └── client
      ├── header.ts - Header web component
      └── board.ts  - Board web component

Components

The project is divided into three main parts:

Client (client.ts): Manages user interaction, communicates with the server, and updates the user interface based on server events.
Server (server.ts): The core logic, handling player actions, updating game state, and sending events back to players.
Interfaces (interface.ts): Defines shared types, enums, and commands for seamless client-server communication.
Core Enums and Types
Shared enums and interfaces are essential for the game’s functionality, defining roles, player states, game actions, and board positions.

Example of key enums:

typescript
Copy code
export enum Piece {
  Dot   = "dot",
  Cross = "cross",
}

export enum Position {
  TopLeft, Top, TopRight, Left, Center, Right, BottomLeft, Bottom, BottomRight
}

export enum PlayerState {
  Joining, WaitingGame, TakingTurn, WaitingTurn, Won, Lost, Tied, Abandoned
}
Client-Server Communication
The Command and Event types represent actions from the client and responses from the server, enabling real-time gameplay via WebSocket. Discriminated unions make it easy to manage actions and events.

Example Command:

typescript
Copy code
export enum Command {
  Join, Turn, Leave, Replay
}

export interface JoinCommand {
  type: Command.Join;
  name: string;
}

export type AnyCommand = JoinCommand | TurnCommand | LeaveCommand | ReplayCommand;
Example Event:

typescript
Copy code
export enum Event {
  PlayerReady, GameStarted, PlayerTookTurn, PlayerWon, PlayerLost, UnexpectedError
}

export interface PlayerReadyEvent {
  type: Event.PlayerReady;
  player: Player;
}
Client Overview
The client is minimal, handling user events and updating the interface. The primary components, Header (header.ts) and Board (board.ts), manage game information display and render the game board, respectively.

Server Overview
The server maintains the game logic, handling player sessions, game state, and player actions. Three primary modules manage the server’s functionality:

Player (player.ts): Manages player states.
Board (board.ts): Manages board state and winning conditions.
Lobby (lobby.ts): Orchestrates gameplay, receiving commands from clients, updating states, and sending events back to players.
The game server also detects disconnections, ensuring smooth multiplayer sessions.

This project’s structure and logic provide a strong foundation for understanding WebSocket-based multiplayer games, offering a straightforward yet engaging experience of real-time gameplay. Enjoy playing or exploring the code to see how each part contributes to the seamless tic-tac-toe experience!

Made with Love by Gideon Bawa