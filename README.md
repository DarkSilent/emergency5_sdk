EMERGENCY 5, 2016, 2017 and 20 SDK 4.2.0 for modding. The EMERGENCY 5 SDK contains addtional tools for modders:
- Plugin SDK (C++) to create game and editor extensions
- Server software for cooperative work on the same mod project
- Demo mods and sample projects as starting point for your own mods and plugins

Visit [World of EMERGENCY](https://www.world-of-emergency.com/modding) for more information.

## Matchmaking SDK notes

The SDK contains matchmaking client headers and packet/data definitions, but it does not document enough server-side behavior to implement a fully compatible custom matchmaking service from the repository alone. See [docs/matchmaking-server.md](docs/matchmaking-server.md) for a summary of what is available and what is still missing.

Due to a GitHub file size limit of 100 MiB, we had to compress the following file: "emergency5_sdk\plugin_api\external\_windows_x64\boost\lib\libboost_wave-mt-gd.lib". Please unzip "libboost_wave-mt-gd.zip" before using the SDK.
