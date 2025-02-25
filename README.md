As of now, the [ryujinx-mirror/ryujinx](https://github.com/ryujinx-mirror/ryujinx) repository serves as a downstream hard-fork of the original Ryujinx project. For the time being, this fork won't be accepting any new *major* changes until further information arises. We have reconstructed the essential build infrastructure, and you can download nightly binaries for Windows, Linux, and MacOS from the [latest release](https://github.com/ryujinx-mirror/ryujinx/releases/latest).

> [!NOTE]
> This fork is not affiliated with the **original** Ryujinx project, or Nintendo whatsoever.

### Current Goals

* ☑️ Reconstruct basic build infrastructure & workflows for this repository, based on revision hashes as opposed to semver releases (for now)
* ☑️ To be as safe as possible, remove all previous in-app and meta references to Patreon, `ryujinx.org` etc while keeping full attribution of original authors and contributors in-tact.
* Keep 'branding' as pure and faithful to the original project as possible. 

### Join Discussion

Feel free to join the [Latte Softworks Discord community](https://latte.to/discord) to join in on the discussion & development of this fork going forward.<br>
See `#ryujinx-info` for more information.

[![Latte Softworks Discord](https://img.shields.io/discord/892211155303538748?label=Latte%20Softworks&logo=discord&logoColor=FFFFFF&color=5865F2)](https://latte.to/discord)

___

<h1 align="center">
  <br>
  <a href="https://github.com/ryujinx-mirror/ryujinx"><img src="distribution/misc/Logo.svg" alt="Ryujinx" width="150"></a>
  <br>
  <b>Ryujinx</b>
  <br>
  <sub><sup><b>(REE-YOU-JINX)</b></sup></sub>
  <br>
</h1>

<p align="center">
  Ryujinx is an open-source Nintendo Switch emulator, created by gdkchan, written in C#.
  This emulator aims at providing excellent accuracy and performance, a user-friendly interface and consistent builds.
  It was written from scratch and development on the project began in September 2017.
  Ryujinx is available on Github under the <a href="LICENSE.txt" target="_blank">MIT license</a>.
  <br />
</p>

## Compatibility

As of May 2024, Ryujinx has been tested on approximately 4,300 titles;
over 4,100 boot past menus and into gameplay, with roughly 3,550 of those being considered playable.

You can check out the compatibility list [here](https://github.com/ryujinx-mirror/Ryujinx-Games-List/issues).

Anyone is free to submit a new game test or update an existing game test entry;
simply follow the new issue template and testing guidelines, or post as a reply to the applicable game issue.
Use the search function to see if a game has been tested already!

## Usage

To run this emulator, your PC must be equipped with at least 8GiB of RAM;
failing to meet this requirement may result in a poor gameplay experience or unexpected crashes.

<!--
See our [Setup & Configuration Guide](https://github.com/ryujinx-mirror/Ryujinx/wiki/Ryujinx-Setup-&-Configuration-Guide) on how to set up the emulator.

For our Local Wireless (LDN) builds, see our [Multiplayer: Local Play/Local Wireless Guide](https://github.com/ryujinx-mirror/Ryujinx/wiki/Multiplayer-(LDN-Local-Wireless)-Guide).
-->

<!--Avalonia UI comes with translations for various languages. See [Crowdin](https://crwd.in/ryujinx) for more information.-->

## Latest build

These builds are compiled automatically for each commit on the master branch.
While we strive to ensure optimal stability and performance prior to pushing an update, our automated builds **may be unstable or completely broken**.

See [the releases page](https://github.com/ryujinx-mirror/ryujinx/releases) for automatic builds for Windows, macOS, and Linux.

<!--
If you want to see details on updates to the emulator, you can visit our [Changelog](https://github.com/ryujinx-mirror/Ryujinx/wiki/Changelog).

The latest automatic build for Windows, macOS, and Linux can be found on the [Official Website](https://ryujinx.org/download).
-->

## Documentation

If you are planning to contribute or just want to learn more about this project please read through our [documentation](docs/README.md).

## Building

If you wish to build the emulator yourself, follow these steps:

### Step 1

Install the [.NET 8.0 (or higher) SDK](https://dotnet.microsoft.com/download/dotnet/8.0).
Make sure your SDK version is higher or equal to the required version specified in [global.json](global.json). 

### Step 2

Either use `git clone https://github.com/ryujinx-mirror/ryujinx` on the command line to clone the repository or use Code --> Download zip button to get the files.

### Step 3

To build Ryujinx, open a command prompt inside the project directory.
You can quickly access it on Windows by holding shift in File Explorer, then right clicking and selecting `Open command window here`.
Then type the following command: `dotnet build -c Release -o build`
the built files will be found in the newly created build directory.

Ryujinx system files are stored in the `Ryujinx` folder.
This folder is located in the user folder, which can be accessed by clicking `Open Ryujinx Folder` under the File menu in the GUI.

## Features

- **Audio**

  Audio output is entirely supported, audio input (microphone) isn't supported.
  We use C# wrappers for [OpenAL](https://openal-soft.org/), and [SDL2](https://www.libsdl.org/) & [libsoundio](http://libsound.io/) as fallbacks.

- **CPU**

  The CPU emulator, ARMeilleure, emulates an ARMv8 CPU and currently has support for most 64-bit ARMv8 and some of the ARMv7 (and older) instructions, including partial 32-bit support.
  It translates the ARM code to a custom IR, performs a few optimizations, and turns that into x86 code.
  There are three memory manager options available depending on the user's preference, leveraging both software-based (slower) and host-mapped modes (much faster).
  The fastest option (host, unchecked) is set by default.
  Ryujinx also features an optional Profiled Persistent Translation Cache, which essentially caches translated functions so that they do not need to be translated every time the game loads. 
  The net result is a significant reduction in load times (the amount of time between launching a game and arriving at the title screen) for nearly every game.
  NOTE: This feature is enabled by default in the Options menu > System tab.
  You must launch the game at least twice to the title screen or beyond before performance improvements are unlocked on the third launch!
  These improvements are permanent and do not require any extra launches going forward.

- **GPU**

  The GPU emulator emulates the Switch's Maxwell GPU using either the OpenGL (version 4.5 minimum), Vulkan, or Metal (via MoltenVK) APIs through a custom build of OpenTK or Silk.NET respectively.
  There are currently six graphics enhancements available to the end user in Ryujinx: Disk Shader Caching, Resolution Scaling, Anti-Aliasing, Scaling Filters (including FSR), Anisotropic Filtering and Aspect Ratio Adjustment.
  These enhancements can be adjusted or toggled as desired in the GUI.

- **Input**

  We currently have support for keyboard, mouse, touch input, JoyCon input support, and nearly all controllers.
  Motion controls are natively supported in most cases; for dual-JoyCon motion support, DS4Windows or BetterJoy are currently required.
  In all scenarios, you can set up everything inside the input configuration menu.

- **DLC & Modifications**

  Ryujinx is able to manage add-on content/downloadable content through the GUI.
  Mods (romfs, exefs, and runtime mods such as cheats) are also supported;
  the GUI contains a shortcut to open the respective mods folder for a particular game.

- **Configuration**

  The emulator has settings for enabling or disabling some logging, remapping controllers, and more.
  You can configure all of them through the graphical interface or manually through the config file, `Config.json`, found in the user folder which can be accessed by clicking `Open Ryujinx Folder` under the File menu in the GUI.

<!--
## Contact

If you have contributions, suggestions, need emulator support or just want to get in touch with the team, join our [Discord server](https://discord.com/invite/Ryujinx).
You may also review our [FAQ](https://github.com/ryujinx-mirror/Ryujinx/wiki/Frequently-Asked-Questions).
-->

## License

This software is licensed under the terms of the [MIT license](LICENSE.txt).
This project makes use of code authored by the libvpx project, licensed under BSD and the ffmpeg project, licensed under LGPLv3.
See [LICENSE.txt](LICENSE.txt) and [THIRDPARTY.md](distribution/legal/THIRDPARTY.md) for more details.

## Credits

- [LibHac](https://github.com/Thealexbarney/LibHac) is used for our file-system.
- [AmiiboAPI](https://www.amiiboapi.com) is used in our Amiibo emulation.
- [ldn_mitm](https://github.com/spacemeowx2/ldn_mitm) is used for one of our available multiplayer modes.
- [ShellLink](https://github.com/securifybv/ShellLink) is used for Windows shortcut generation.
