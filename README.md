# spectre_test_from_paper

The Spectre security vulnerability paper from Kocher et al.: [Spectre Attacks: Exploiting Speculative Execution](https://spectreattack.com/spectre.pdf).

In section 4.2, Kocher et al. describe an example implementation in C. Which is also included in Appendix A in the paper. The code included here is equal to the code from the paper in exception of a few fixes to make it work in my environment. 

### What am I using?
CPU: [i5-6267U](https://ark.intel.com/products/91166/Intel-Core-i5-6267U-Processor-4M-Cache-up-to-3_30-GHz)

OS: MacOS High Siera (10.13.2) with [the latest security update](https://support.apple.com/en-us/HT208397) (as of 2018/01/09 11:30)

### How to run?
If you don't have it, install GCC

Then run the following commands. Depending on environment you might have to fix warnings and/or change the CACHE_HIT_THRESHOLD in spectre_example.c.

Compile:
`gcc -o spectre spectre_example.c`

Then run:
`./spectre`

### Results:
After running, you'll probably see the following. This basically shows my version of MacOS in combination with my CPU are still vulnerable (2018/01/09). Hopefully, the vulnerability has been fixed when you're trying, and the results look very different. (Note: It shows spectre has, at least in part, not been "succesfully" patched because the "secret" message "The Magic Words are Squeamish Ossifrage." has been read.)
<img src="https://github.com/HyHend/spectre_test_from_paper/blob/master/screenshot.png" width="600px" alt="Screenshot">

### Concequences:
Spectre is an issue resulting in very low level hardware design decisions and might not be fixable in existing hardware. Patches from CPU manufacturers could include changes in each CPU's [opcode](https://en.wikipedia.org/wiki/Opcode) set. Possibly disallowing operations which could lead to the misuse of branch prediction and speculalive execution. Misuse of vulnerabilities can also be prevented on an operating system, compiler and/or even application level (Browsers, for example). 

### Accidentally going into opinionated stuff. I'll make that clear with a header:
In my opinion, the further away from the problem (CPU), the least impact the fix has on the actual problem. A browser fixing it will only fix it specifically for them and not for all other browsers, programs. (Why browser?: The paper also shows in part a JavaScript implementation allowing JS code to retrieve information from the lower level process. Which for example is also running your other tab with a banking website).

There is a larger underlying problem to these vulnerabilities. Spectre, meltdown, bluecoat, heartbleed, etc.. These are the found ones. Software (and, apparently hardware also ;)) is written by people. Mere humans like you and me, and we all know we make mistakes. We accidentally write bugs into code. We think hard. We try to find all possible downsides in an awesome invention like speculative execution. But we don't think of everything! There's no situation in which a 100% coverage of flaws has been found. 

Therefore, there are bugs, there are vulnerabilities with an impact beyond what we can even think of. They are there. Some we know of, a lot nobody (literally no one on earth) knows about. Spectre is not the first one and will not be the last one.

What can we do with this information? Is doing the rat race of finding and fixing problems an optimal solution or can we do better?