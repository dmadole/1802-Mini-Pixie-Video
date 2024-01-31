# 1802/Mini Pixie Differences

While the Pixie video card is designed to be compatible with existing software for the CDP1861, there are some
significant differences and improvements in this implementation.

The sync output is improved and is now completely uniform with falling horizontal pulse edges always equally
spaced, and a three-line vertical sync pulse. This avoids horizontal tearing at the top of the display that
can occur on certain monitors and configurations.

The dot clock and processor clock are asynchronous. The video card pauses the processor by asserting WAIT to
maintain synchronization rather than forcing the processor to run at the dot clock frequency. When displaying
video, the effective processor speed is 1.79 MHz due to the wait states so that games still run at the proper
speed. But when video is off the machine runs at normal full clock rate.

There is a jumper-selectable option to only assert wait states during the active display area and run at full
speed otherwise. To allow for syncronization prior to and during the interrupt service routine, the wait cycles
are actually introced 16 scan lines before the 128-line display area, so for 144 lines of 262 in total.

Instead of skipping a horizontal count to bring the processor machine cycle into sync with the display like the
1861, the card instead inserts additional wait time on the processor. This means that the horizonal rate never
changes even when three-cycle instructions cause misalignment, so the display never loses synchronization. This
may allow use of three-cycle instructions outside the interrupt service routine (actually in the interrupt service
routine also but there is really no need to).

The centering of the display area is improved over the 1861, particularly in the horizonal direction, where the
1861 tended to have the image shifted to the right. The exact position will vary slightly from monitor to monitor.

There is an 8-pin connector that is intended to connect to a possible future expansion card to plement CDP1862-
compatible color video. Until that card is designed this connector has no practical purpose. It does not output
color video in any form.

The I/O port is fixed at port 1, with INP 1 enabling video and OUT 1 disabling video. This is compatible with
the VIP and Studio II machines and some other implementations. It is possible to use group select as well.
