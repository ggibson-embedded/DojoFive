# DojoFive
Interview Challenge

For me the Practical Challenge was a bit more difficult than it likely was for other people as I have not used any of the tools that were involved in any of the challenges. I had never used Github until now but I am impressed with all of these tools so far.

I chose Option 3: Simultate All The Things. I found the documentation on renode pretty thorough and relatively easy to follow. After installing the first major snag I hit was when I set up an environment for STM32 or nRF52 devices I received errors that it failed to download due to SecureChannelFailure. I was unable to find much information about what the cause of this issue could be.

Running Renode program:
Open renode
type "s @scripts/single-node/nrf52840.resc" to start nRF52840

Looking into this SecureChannelFailure issue more I found there is an open issue on github with this same problem on similar systems as mine, Issue #251. Issue was reported on September, October 8 and October 18. Resolution seems to be getting the renode-latest.msi and using that instead. After the right combination of uninstall, restart and reinstall I was able to get the renode system to start properly and be able to load the correct machine.

Once I finally had Renode through that issue I downloaded and installed all of the necessary components for compiling a nRF52 project in VS code. Upon successfully building a helloworld application placed the .elf file from that application in Renode folder ran the following commands in nrf52840.resc.

using sysbus

mach create
machine LoadPlatformDescription @platforms/cpus/nrf52840.repl

$bin?=@zephyr.elf

showAnalyzer uart0

macro reset
"""
    sysbus LoadELF $bin
"""
runMacro $reset

