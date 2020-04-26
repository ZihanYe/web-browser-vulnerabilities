# Reproducing Firefox vulnerabilities

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

    ```
    export MOZCONFIG=/path/to/your/mozconfig
    ```

## Build
   ```
          ./mach bootstrap
          ./mach build
   ```
   
## Troubleshooting

:point_right: [:link:](troubleshooting.md)
