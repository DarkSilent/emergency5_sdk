# Custom matchmaking server support in this SDK

Short answer: **no, not completely**.

This repository exposes parts of the matchmaking client API, but it does **not** contain a complete specification for building your own fully compatible matchmaking backend.

## What the SDK does provide

The following headers show which kinds of requests and responses exist on the client side:

- `plugin_api/em5/em5/network/matchmaking/MatchmakingClient.h`
- `plugin_api/em5/em5/network/matchmaking/MatchmakingProtocol.h`
- `plugin_api/em5/em5/network/matchmaking/MatchmakingTypes.h`
- `plugin_api/em5/em5/network/matchmaking/packet/RegisterHostRequest.h`
- `plugin_api/em5/em5/network/matchmaking/packet/RegisterHostResponse.h`
- `plugin_api/em5/em5/network/matchmaking/packet/UpdateHost.h`
- `plugin_api/em5/em5/network/matchmaking/packet/UnregisterHost.h`
- `plugin_api/em5/em5/network/matchmaking/packet/HostListRequest.h`
- `plugin_api/em5/em5/network/matchmaking/packet/HostList.h`
- `plugin_api/em5/em5/network/matchmaking/packet/TestOpenPortRequest.h`
- `plugin_api/em5/em5/network/matchmaking/packet/TestOpenPortResponse.h`
- `plugin_api/em5/em5/network/matchmaking/packet/ProxyServerPropertiesRequest.h`
- `plugin_api/em5/em5/network/matchmaking/packet/ProxyServerPropertiesResponse.h`

From these headers you can infer that the game expects support for:

- host registration and unregistration
- host updates
- host list queries
- open-port checks
- proxy server property queries

You can also see the client-side data model in `MatchmakingTypes.h`, including `HostEntry`, `RegisterHostStatus`, `GameMode`, proxy session information, and IPv4/IPv6-related fields.

## What is missing

The repository does not document several pieces that are needed for an independent server implementation:

- the authoritative wire-level protocol description
- the numeric values behind `PROTOCOL_ID` and the matchmaking packet `PACKET_ID`s
- connection bootstrap details such as expected endpoint configuration, version negotiation, authentication, and compatibility checks
- lifecycle rules such as heartbeats, timeouts, host expiry, reconnect behavior, and update frequency
- server-side validation rules for `HostEntry` fields
- the exact behavior expected from proxy integration and proxy session management
- a reference matchmaking server implementation or end-to-end example

There is also an explicit documentation gap in the headers themselves: several matchmaking packet classes still contain `TODO(co) Comment me` instead of protocol documentation.

## Practical conclusion

If your goal is to understand roughly which matchmaking features exist, the SDK is useful.

If your goal is to build a **drop-in compatible custom matchmaking server**, the SDK documentation in this repository is **not sufficient on its own**. You would still need additional information, such as:

- internal documentation for the original matchmaking service
- implementation sources for the original server
- binary/protocol reverse engineering
- real-world traffic captures from a known-compatible environment

## Recommended next step

Treat the matchmaking headers in this repository as a partial client contract, not as a complete backend specification. Any serious custom server effort should first close the missing protocol and server-behavior gaps listed above.
