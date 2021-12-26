A vscode project template for **Nordic nrf5 SoC**
====

## Directory Layout
```
├── vscode
│   ├── c_cpp_properties.json
│   ├── launch.json
│   ├── settings.json
│   └── tasks.json
├── boards <- Add your boards configurations here.
│   └── pca10040e
│       └── s112
│           ├── armgcc
│           │   ├── ble_app_template_gcc_nrf52.ld
│           │   ├── _build <- The built artifacts goes here.
│           │   └── Makefile
│           └── config
│               └── sdk_config.h <- The CMSIS sdk config.
├── nrf_sdk -> ../nordic/sdk <- The symbolic link to your nrf5 SDK dir.
├── README.md
├── src <- All your source code.
│   └── main.c
└── tools <- The config files for external tools such as openocd.
    ├── daplink.cfg
    ├── jlink-ob.cfg
    └── PROGRAM_WITH_OPENOCD.md
```

## How to use the template
1. Install the dev tools
   ```
   nrf sdk
   nrfutils
   arm gcc toolchain (Create an env varible `ARM_GCC` to point to the root dir of your toolchain)
   gdb-multiarch
   JLink command line tools
   JRE (In case you need the CMSIS Configuration Wizard.)
   Visual Studio Code
   openocd (optional)
   ```

2. Add or modify the board config in the **boards** dir based on your project (board, softdevice, Makefile).
   A sample could be found in the nrf SDK.

   Modify the basic settings in `.vscode/setting.json`
   ```{json}
   {
       "board": "pca10040e",
       "softdevice": "s112",
       "nrf_sdk_root": "${workspaceRoot}/nrf_sdk",
       ...
   }
   ```
   You may also need to check the connection settings for your debug probe in `.vscode/launch.js` 

3. Start the vscode from the project root directory.
   ```
   $ code .
   ```

4. Add your own code to the `src` dir.

5. Run the build tasks in vscode.
   The following tasks are supported, which are defined in the Makefile.
   ```
   erase
   build
   flash
   flash_softdevice
   sdk_config
   ```
   You may modify the `.vscode/tasks.json` to change the task definitions.

6. Debug
   To debug within vscode, you need to install the **cortex-debug** extension.
   There are two debug configurations for vscode.
   - GDB over J-Link
   - GDB over openocd

   These targets are identical. Both works for the J-Link probe.
   If you have a DAPLink probe, just modify the settings of `GDB over openocd`, which is located in `.vscode/launch.json`. Replace the `configFiles` to `daplink.cfg`.
   
