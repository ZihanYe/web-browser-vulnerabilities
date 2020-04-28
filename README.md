# web-browser-vulnerabilities

Steps for building old versions of Firefox: [:link:](Firefox/)

Steps for building old versions of Chrome:


## Firefox vulnerabilities
This is a list of vulnerabilities that is reproducible in old versions of Firefox :point_down:

| CVE ID  | Version | Type | Exploited? | Link|
| ---| --- | ---| ---| --- |
| CVE-2017-7784  | 56.0  | UAF | |[:link:](Firefox/CVE-2017-7784)|
| CVE-2017-7828  | 56.0  | UAF | |[:link:](Firefox/CVE-2017-7828)|
| CVE-2018-5093  | 57.0  | heap buffer overflow | |[:link:](Firefox/CVE-2018-5093)|
| CVE-2018-5094  | 57.0  | heap buffer overflow | | [:link:](Firefox/CVE-2018-5094)|
| CVE-2018-5097  | 56.0/57.0  | UAF | | [:link:](Firefox/CVE-2018-5097)|
| CVE-2018-5100  | 56.0/57.0  | UAF | | [:link:](Firefox/CVE-2018-5100)|
| CVE-2018-5102 | 56.0/57.0  | UAF | | [:link:](Firefox/CVE-2018-5102)|
| CVE-2018-5104  | 56.0/57.0  | UAF | | [:link:](Firefox/CVE-2018-5104)|
| CVE-2018-5127  | 57.0  | heap buffer overflow | |[:link:](Firefox/CVE-2018-5127)|
| CVE-2018-5129  | 57.0  | OOB | |[:link:](Firefox/CVE-2018-5129)|
| CVE-2018-12386  | < 61.0  | type confusion | Yes |[:link:](Firefox/CVE-2018-12386)|
| CVE-2018-12387  | < 61.0 | info leak | Yes |[:link:](Firefox/CVE-2018-12387)|
| CVE-2018-18492  | 62.0/63.0 | UAF | |[:link:](Firefox/CVE-2018-18492)|
| CVE-2019-9791 | < 66.0 | type confusion | Yes |[:link:](Firefox/CVE-2019-9791)|
| CVE-2019-9813 | < 66.0.1 | type confusion | |[:link:](Firefox/CVE-2019-9813)|
| CVE-2019-11707 | < 66.0.3 | type confusion | Yes |[:link:](Firefox/CVE-2019-11707)|

Others to be verified: :point_right: [:link:](Firefox/others/)


## Chrome vulnerabilities
Vulnerabilities in Chrome :point_down:

| CVE ID  | Version | Type | Exploited? | Link|
| ---| --- | ---| ---| --- |
| CVE-2018-6060 | 62.0.3202.75 | UAF | | [:link:](Chrome/CVE-2018-6060)
| CVE-2018-6123 | 68.0.3404.0 | UAF | | [:link:](Chrome/CVE-2018-6123)
| CVE-2019-5786 | 72.0.3626.119 | UAF | | [:link:](Chrome/CVE-2019-5786)
| CVE-2019-5808 | 74.0.3728.0 | UAF | | [:link:](Chrome/CVE-2019-5808)


## Useful links:

## General:

- [Good place for searching CVEs](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=firefox)

- [List of Javascript Engine vulnerabilities](https://github.com/tunz/js-vuln-db)

- [Exploitation DB](https://www.exploit-db.com/)

- [Awesome-browser-exploit](https://github.com/Escapingbug/awesome-browser-exploit)

## Firefox:

### Basic

- [Build configuration](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/Configuring_Build_Options)

- [Build with Address Sanitizer](https://firefox-source-docs.mozilla.org/tools/sanitizer/asan.html)

- [Hacking tips](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/Hacking_Tips)

- [Security Advisories (for finding vulnerabilities)](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)

- [Online code browse](https://searchfox.org/mozilla-beta/source)

### Tutorials

- [Shadow over Firefox](http://www.phrack.org/issues/69/14.html)

- [Jemalloc](https://medium.com/iskakaushik/eli5-jemalloc-e9bd412abd70)

- [Jemalloc Exploitation](http://www.phrack.org/issues/68/10.html#article)

- [Introduction to Spidermonkey exploitation](https://doar-e.github.io/blog/2018/11/19/introduction-to-spidermonkey-exploitation/)

- [Heap manipulation](https://www.usenix.org/legacy/event/woot08/tech/full_papers/daniel/daniel_html/index.html)

- [Spraying the Heap (Chapter 2: Use-After-Free) – Finding a needle in a Haystack](https://www.fuzzysecurity.com/tutorials/expDev/11.html)

- [Heap spray](https://www.corelan.be/index.php/2013/02/19/deps-precise-heap-spray-on-firefox-and-ie10/)

### Exploitation writeups

- [CVE-2012-0469: UAF](http://web.archive.org/web/20150121031623/http://www.vupen.com/blog/20120625.Advanced_Exploitation_of_Mozilla_Firefox_UaF_CVE-2012-0469.php)

- [CVE-2016-9066: cross-map overflow](https://saelo.github.io/posts/firefox-script-loader-overflow.html)

- [CVE-2016-9079: UAF](https://dangokyo.me/2018/07/29/analysis-on-cve-2016-9079/)

- [CVE-2016-1960: UAF exploitation](https://www.exploit-db.com/exploits/42484)

- [CVE-2017-5375: JIT spray RCE](https://www.exploit-db.com/exploits/44293)

- [CVE-2017-5375: JIT spray writeup](https://rh0dev.github.io/blog/2017/the-return-of-the-jit/)

- [CVE-2018-18500: UAF](https://news.sophos.com/en-us/2019/04/18/protected-cve-2018-18500-heap-write-after-free-in-firefox-analysis-and-exploitation/)

- [CVE-2019-9791: Type confusion](https://bugs.chromium.org/p/project-zero/issues/detail?id=1791)

- [CVE-2019-9810, IonMonkey](https://doar-e.github.io/blog/2019/06/17/a-journey-into-ionmonkey-root-causing-cve-2019-9810/)

- [CVE-2019-9813: Type confusion](https://www.exploit-db.com/exploits/46646)

- [CVE-2019-11707: Type confusion](https://blog.bi0s.in/2019/08/18/Pwn/Browser-Exploitation/cve-2019-11707-writeup/)


## Chrome

### General

- [Build configuration](https://gitlab.com/noencoding/OS-X-Chromium-with-proprietary-codecs/-/wikis/List-of-all-gn-arguments-for-Chromium-build)

- [List of command line options](https://peter.sh/experiments/chromium-command-line-switches/)

- [How Blink works](https://docs.google.com/document/d/1aitSOucL0VHZa9Z2vbRJSyAIsAz24kX8LFByQ5xQnUg/edit?pli=1#)

- [Allocator](https://chromium.googlesource.com/chromium/src/base/+show/master/allocator/README.md)

- [Debugging in Linux](https://chromium.googlesource.com/chromium/src/+/81c0fc6d4/docs/linux_debugging.md)

### Exploitation writeup

- [CVE-2019-5786](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/analysis-of-a-chrome-zero-day-cve-2019-5786/)

Happy Hacking :trollface: