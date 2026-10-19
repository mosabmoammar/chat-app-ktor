# Real-Time Chat App (Android client)

An Android chat client built with Kotlin and Jetpack Compose that talks to a Ktor backend over WebSockets. Users pick a username, join the chat room, load the message history, and send and receive messages in real time.

The matching server is in [ktor-server-chat](https://github.com/mosabmoammar/ktor-server-chat).

<!--
Screenshots: add the username screen and the chat screen, for example:
<p float="left">
  <img src="screenshots/username.png" width="220" />
  <img src="screenshots/chat.png" width="220" />
</p>
-->

## Features

- Username screen that opens a WebSocket session for that user
- Message history loaded over REST when the chat opens
- Live messages pushed through the WebSocket and shown instantly
- Own messages and other users' messages styled differently
- Session closed cleanly when the user leaves the screen

## Tech stack

| Area | Tools |
|---|---|
| UI | Jetpack Compose, Material 3, Navigation Compose |
| Architecture | MVVM with a data / domain / presentation split |
| Dependency injection | Hilt |
| Networking | Ktor Client (CIO engine, WebSockets, logging) |
| Serialization | kotlinx.serialization |
| Async | Kotlin Coroutines and Flow |

## Architecture

```
com.mosab.chat/
├── data/remote/       # ChatSocketService (WebSocket), MessageService (REST), DTOs
├── domain/model/      # Message
├── presentation/
│   ├── username/      # username screen and ViewModel
│   └── chat/          # chat screen, ViewModel and state
├── di/                # Hilt AppModule (HttpClient and services)
└── util/              # Resource wrapper
```

`ChatSocketService` exposes incoming messages as a `Flow`, which the chat ViewModel collects into its state.

## Getting started

1. Run the server from [ktor-server-chat](https://github.com/mosabmoammar/ktor-server-chat).
2. Set `BASE_URL` in `ChatSocketService` and `MessageService` to your server address (for example `ws://10.0.2.2:8080` on the Android emulator).
3. Open the project in Android Studio and run the `app` configuration (API 24 or newer).
