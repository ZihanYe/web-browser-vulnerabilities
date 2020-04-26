# Troubleshooting

:hammer_and_pick::hammer_and_pick::hammer_and_pick::hammer_and_pick::hammer_and_pick:

I have run into many errors especially when trying to build older versions of Firefox (it was painful). Below are solutions I found.


1. **Could not find gconf-2.0**
```
  sudo apt-get install gconf-2.0
  sudo apt-get install -y libgconf2-dev
```

***

2. **configure error with sed 4.3: sed: character class syntax is [[:space:]], not [:space:]**

  - open build/autoconf/icu.m4
  
  - modify manually according to https://bugzilla.mozilla.org/attachment.cgi?id=8825307&action=diff

***

3. **anything with rustc/cargo version:**

  It is likely because we are using newer version of rustc now and we need to downgrade it.
  
  - Find rustc version used at the time of the older version in [Firefox's Rust Update policy](https://wiki.mozilla.org/Rust_Update_Policy_for_Firefox)

  **Either:**
  
  - run ```$ ~/.cargo/bin/rustup self uninstall```
  
  - install:  
    ```
      $ curl https://sh.rustup.rs -sSf | sh
       Choose:
         2) Custom Installation
            default host triple <enter>
            default toolchain  1.22.1
            Modify PATH variable? (y/n)  n
       Then Choose:
         1) Proceed with installation (default)
    ```
    
  **or** 
  - install rustup and

  - ```rustup default <version>```

    For Firefox 57.0, I had to downgrade rustc to 1.19.0.
    
    For Firefox 63.0.3, I had to downgrade rustc to 1.28.0.

***
    
4. **ASAN build reports gcc compilation error:**

  ```error: inlining failed in call to always_inline ‘memcpy’: function attribute mismatch \__NTH (memcpy (void *\__restrict \__dest, const void *\__restrict \__src,```

  See https://bugzilla.mozilla.org/show_bug.cgi?id=1422254
  
  Basically add `-U_FORTIFY_SOURCE` to CFLAGS and CXXFLAGS in mozconfig
  
***

5. **Compiler error: undefined reference to dlsym**

  see https://askubuntu.com/questions/454443/how-do-i-deal-with-undefined-reference-to-dlopen-errors-while-compiling-and-us
  
  add `-Wl,--no-as-needed -ldl` to LDFLAGS in mozconfig
  
***

6. During a build with option ---enable-fuzzing, I got **gtest error**
  
   ```Firefox fatal error: gtest/gtest.h: No such file or directory```
   
   I fixed this by adding option --enable-tests
 
***
 
7. During a build with option --enable-fuzzing, I got **error in TestCodeGenBinding**
  
   ```dom/bindings/TestCodeGenBinding.cpp:34165:9: error: 'class mozilla::dom::TestInterface' has no member named 'PassUnion2'```
   
   https://bugzilla.mozilla.org/show_bug.cgi?id=1293516 mentions this error.
   
   I fixed it with running ```./mach clobber``` and rebuild.

*** 
 
8. **Llvm-config: checking for llvm-config... not found**

  install llvm-config, check if it exists in /usr/bin/
  Add to mozconfig a line: ```export LLVM_CONFIG=“/usr/bin/llvm-config”```

***

9. **clang**

  Sudo apt install clang

***

10. **nodejs version not new enough**

  uninstall nodejs: sudo apt remove nodejs
  install nodejs: 
  
  ```https://deb.nodesource.com/setup_8.x | sudo -E bash -```
  
  ```sudo apt-get install -y nodejs```

***

11. Firefox 56 and 59 crashes at startup with:

> Assertion failure: false, at /home/user/firefox/security/sandbox/linux/SandboxInfo.cpp:174

[Bug report](https://bugzilla.mozilla.org/show_bug.cgi?id=1430756)

Change according to the [fix](https://hg.mozilla.org/mozilla-central/rev/22ce3b9ca9af)
