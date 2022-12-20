# Render96ex macOS Edition
Fork of [Render96ex](https://github.com/Render96/Render96ex) meant to run on macOS (Intel and Apple Silicon hardware)

I'll try to keep this repo reasonably up-to-date with both Render96ex tester branch and
[sm64ex](https://github.com/sm64pc/sm64ex) nightly branch, but I'm not promising anything.

* If you want to help sm64ex then go to their repo.
* If you want to help Render96ex go to their repo.
* If you want to help here just open a PR.

## Build instructions

1. Obtain a legal copy of the following Super Mario 64 ROM

    * sm64.us.z64 `sha1: 9bef1128717f958171a4afac3ed78ee2bb4e86ce`

   This repo does not include all assets necessary for compiling the ROMs.\
   A prior copy of the game is required to extract the assets.\
   Please don't ask for a copy of the game.

2. Rename the ROM to `baserom.us.z64` and place it into the repository's root directory.

3. Install dependencies

   Install [Homebrew](https://brew.sh/) if you don't have it already:

    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

   Install the following dependencies:
    ```
    brew update
    brew install make mingw-w64 gcc sdl2 pkg-config glew glfw3 libusb
    ```

   \* Tested with GCC 12.2.0

4. Build the ROM

   Use Homebrew's GNU make because the version included with macOS is too old.

    ```
    gmake -j4
    ```

   For extra features check [Render96's Build Arguments](https://github.com/Render96/Render96ex/wiki/Build-Arguments).

   In this repo  the flags `OSX_BUILD` and `TEXTURE_FIX` are enabled by default.
   I have only tested with `VERSION=US` (which is also the default).

5. To start the game run the generated executable:
    ```
    cd build/us_pc/
    ./sm64.us.f3dex2e
    ```
6. (Optional) Combine the model pack:
    1. Obtain the latest release of the model pack. It can be found under https://github.com/Render96/ModelPack/releases (Render96_DynOs_v3.2.7z)
    2. Extract the contents of the .7z file into `./build/us_pc/dynos/packs`

7. (Optional) Combine the model pack:
    1. Obtain the latest version of the texture pack.
        ```
        git clone https://github.com/pokeheadroom/RENDER96-HD-TEXTURE-PACK.git -b master
        ```
    2. Copy the contents of the `gfx` folder within the texture pack into `./build/us_pc/res/gfx/`


### Check Render96's wiki page for in depth help on compiling
https://github.com/Render96/Render96ex/wiki

## TODO (Help wanted)

- [ ] Make `tester` and `tester_rt64alpha` branches.\
  The main blocker ATM is getting https://miniaud.io/ to build under Homebrew's version of GCC.
- [ ] Modify the build process to generate a macOS Application Bundle.\
  This is important as I haven't found a good macOS compatible launcher for Render96.\
  I already have a solution for this, but I'm currently waiting for authorization to use some artwork.\
  For now folks will have to make do with a solution such as https://github.com/machinebox/appify and a script like:
  ```
  #!/usr/bin/env bash
  cd /path/to/Render96ex_macOS/build/us_pc
  ./sm64.us.f3dex2e
  ```
- [x] Contribute M1 specific build fixes to https://github.com/sm64pc/sm64ex
- [ ] Contribute relevant changes back to https://github.com/Render96/Render96ex.\
  Definitely need to get `tester` and `tester_rt64alpha` to build for this one (`alpha` is somewhat abandoned).
