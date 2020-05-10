# Reproducing Firefox vulnerabilities

[Getting the code](#getting-the-code)

[Configuration](#configuration)

[Build](#build)

[Troubleshooting during build](#troubleshooting_during_build)

[Make JS Shell](#make_js_shell_optional)

[Hack](#hack)

[Run](#run)

OS: Ubuntu 64-bit

## Getting the code

Two ways:

:one: Get from Mercurial repository:

```
hg clone https://hg.mozilla.org/releases/mozilla-release/ <foldername> -u <revision>
```

where <revision> is the changeset hash found in [here](https://hg.mozilla.org/releases/mozilla-release/tags),
and if switching to another changeset:
```
hg update -r <revision>
```

:two: download from https://ftp.mozilla.org/pub/firefox/releases/


## Configuration

### normal debug build:
    ```
    echo "# for debug" > mozconfig
    echo "ac_add_options --disable-optimize" >> mozconfig
    echo "ac_add_options --enable-debug" >> mozconfig
    ```

an example mozconfig :point_right: [:link:](mozconfig_dbg)

### ASAN build:

see https://developer.mozilla.org/en-US/docs/Mozilla/Testing/Firefox_and_Address_Sanitizer

an example mozconfig :point_right: [:link:](mozconfig)

## Build

Specified a mozconfig file for build:
```
export MOZCONFIG=/path/to/your/mozconfig
```

run:
```
./mach bootstrap
./mach build
```
   
## Troubleshooting during build

:point_right: [:link:](troubleshooting.md)

## Make JS Shell (optional)
  ```
  cd js/src
  autoconf2.13

  # This name should end with "_DBG.OBJ" to make the version control system ignore it.
  mkdir build_DBG.OBJ
  cd build_DBG.OBJ
  ../configure --enable-debug --disable-optimize
  # Use "mozmake" on Windows
  make
  ```

## Hack

### **disable hardening flags**

Hardening flags are set in ```./build/moz.configure/toolchain.configure```

Flag that disables stack canary: ```-fno-stack-protector```

### **expose garbage collection interface**

To expose the garbage collection function to JavaScript, below are files needed for change:

- ./dom/bindings/Bindings.conf

- ./dom/base/moz.build

- ./dom/webidl/moz.build

- ./dom/webidl/FuzzingFunctions.webidl

Revisions that added the function with ```--enable-fuzzing``` flags:

https://hg.mozilla.org/integration/autoland/rev/80a323cabf56

https://bugzilla.mozilla.org/show_bug.cgi?id=1322400

https://hg.mozilla.org/mozreview/gecko/rev/f8b273c4a7169d8a4dcdf1bcc591f2b0dec240a9


## Run

Run Firefox in headless mode:

In order for making Firefox opening the PoC file without any other disruption, some preferences need to be added. 

Create a new profile:

```
mkdir -p /path/to/firefox/build/directory/tmp/customized_profile
```

create a file called ```user.js``` in the folder. Add preferences inside ```user.js```.

Useful preferences include:

```
user_pref("browser.shell.checkDefaultBrowser", false);
user_pref("general.warnOnAboutConfig", false);
user_pref("fuzzing.enabled", true);
user_pref("browser.tabs.remote.autostart", false);
user_pref("security.sandbox.content.level", 1);
user_pref("toolkit.startup.max_resumed_crashes", -1);
user_pref("browser.startup.page", 0);
user_pref("browser.shell.checkDefaultBrowser", false);
user_pref("browser.sessionstore.resume_from_crash", false);
user_pref("browser.tabs.warnOnOpen", false);
user_pref("browser.tabs.warnOnClose", false);
user_pref("security.insecure_field_warning.contextual.enabled", false);
user_pref("security.insecure_password.ui.enabled", false);

```

Run firefox with options ```--headless --no-remote --profile /path/to/the/profile/folder/just/created file:///path/to/crash.html```



