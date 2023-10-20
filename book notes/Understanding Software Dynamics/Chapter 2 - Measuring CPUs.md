- if you are not familiar with the terms _instruction fetch_, _pipelining_, _cache memory_, and _virtual memory_, now would be a good time to review a computer architecture book such as [Hennessy and Patterson](https://www.amazon.com/dp/B078MFDTX4/)
	- I'm... kind of familiar? Let's plow ahead and see how we do

- Brief overview of the history when each of the major CPU speedup mechanisms arose
- They are:
	- decoupled CPU and memory clocks
	- Multiple memory banks
	- Multiple data registers
	- Multiple instructions per word
	- Instruction pipelining
	- Multiple execution units
	- Speculative execution
	- Multiple instruction issue
	- Out of order execution
	- Cache memory (L1 (I - Instruction & D - Data), L2, L3...)
	- Paged virtual memory
	- Simultaneous multithreading

```
┌─┬──────┐
│ ├──────┴─┐                       ┌──────┐
│ │Multiple│                    ┌──►Issue ├───┐
└─┤  PCs   │                    │  │ Slot │   │
  └───┬────┘                    │  └──────┘   │
      │                         │             │    ┌───────┐
      │                         │  ┌──────┐   │    │┼┼┼┼┼┼┼┼─┐
      │          ┌──────────┐   │  │Issue │   │    │┼┼───────┴─┐  ┌────────────┐
┌─────▼──────┐   │Decode &  ├───┼──► Slot ├───┼───►└┼│Execution└──► L1 D-cache │
│ L1 I-cache ├───►  Buffers │   │  └──────┘   │     └┤  units  ◄──┐            │
└───┬─▲──────┘   └──────────┘   │             │      └─────────┘  └───▲────┬───┘
    │ │                         │  ┌──────┐   │                       │    │
┌───▼─┴────┐                    ├──►Issue ├───┤                    ┌──┴────▼──┐
│ L2 cache │                    │  │ Slot │   │                    │ L2 cache │
└──────────┘                    │  └──────┘   │                    └──────────┘
                                │             │
                                │  ┌──────┐   │
                                └──►Issue ├───┘
                                   │ Slot │
                                   └──────┘

```

> Software that accidentally defeats some of these speedup mechanisms can run unexpectedly slowly, producing performance surprises

The _latency of an instruction_ is the number of CPU cycles from its first "execute" cycle to the first "execute" cycle of a subsequent instruction that uses the result

However, the latency of a _branch_ instruction is the number of CPU cycles from fetching the instruction to fetching its successor

To measure the latency of an **add** instruction, we want to do something like this:

```
read the time
execute an add
read the time
subtract the two times
```

Older CPUs had a simple cycle counter, which was easily convertible to real time; just multiply cycles by picoseconds per cycle. However, in 2002 techniques were introduced to save power by dynamically slowing down the CPU clock - make cycle count not easily convertible to real time.

Thus, CPUs changed to a "constant-rate" timestamp counter. For ex, a CPU might have a counter that increments by 24 at 100mhz on a 2.4ghz chip, regardless of whether it's power-throttled down to 800mhz or overclocked to 2.7ghz. This gives consistent real time measurements, but does not count CPU cycles and also greatly lowers the resolution of the counter.

Thus to do benchmarking of an add, we'll need to:
- do tens of thousands of cycles of work between timestamp instructions
- measure only when the CPU is busy enough to avoid power-saving
- ensure that the duration of work is at least 1000nsec to combat the distortion from the low resolution timer

Our pseudocode is now:
```
read time
execute N adds
read time
subtract the times and divide by N
```

There are lots of ways to fail at this.

## we could try not using a loop:
```
sum += 1
sum += 1
sum += 1
```

but we might only end up measuring instruction fetch from the i-cache or memory

## we could write a loop (`RDTSC` is the timestamp instruction on x86 assembly):
```
start = RDTSC();
for (int n=0; n < 5000; ++n) {
	sum += 1
}
delta = RDTSC() - start;
```

and then divide. But the loop brings a lot of instructions with it - increment, compare, conditional-branch.

**diversion**: how do I run an x86 C program on my arm mac?
- `docker run --rm -it --platform=linux/amd64 -v ${PWD}:/book gcc:latest bash`

- What is your order-of-magnitude estimate of how long you expect an add to take?
	- 1 cycle
```shell
$ gcc mystery0.cc
$ ./a.out
1000000000 iterations, 2160802918 cycles, 2.16 cycles/iteration
```

- The author's machine gave 6.76! Then he compiled with O2 and got... 120 cycles total
	- I got 83 cycles on O2

Here's the relevant assembly from my version of gcc:
- We can get assembly output from gcc with:
	- `gcc -S -o main.s main.c`
- or just print it to stdout with
	- `gcc -S -o - main.c`
- one note: `.cc` is detected by gcc as a c++ file extension, I had only previously used `.cpp`


```
    rdtsc                              ; read timestamp
	salq	$32, %rdx                  ; shift left quadword
	orq	    %rdx, %rax                 ; or quadword
	movq	%rax, -24(%rbp)            ; move quadword rax to startcy in memory
	movl	$0, -12(%rbp)              ; move longword 0 to i in memory
	                                   ; -- here start the differences --
	jmp	.L2                            ; jump to L2
.L3:                                   ; 
	addq	$1, -8(%rbp)               ; add one to sum
	addl	$1, -12(%rbp)              ; add one to i
.L2:                                   ; 
	cmpl	$999999999, -12(%rbp)      ; if i is less than kIterations,
	jle	.L3                            ; jump to L3
	rdtsc                              ; read final timestamp
	salq	$32, %rdx                  ; shift left quadword
	orq	%rdx, %rax                     ; or quadword

```

On `O2`, to nobody's surprise, gcc eliminates the useless loop

``` asm
	rdtsc
	movq	%rax, %rsi
	salq	$32, %rdx
	orq	    %rdx, %rsi
	rdtsc
	movq	stdout(%rip), %rdi
	pxor	%xmm0, %xmm0
	salq	$32, %rdx
	orq	%rdx, %rax
```

## we could try to use a constant the compiler doesn't know
sometimes this hack is useful:
``` C
time_t = time(NULL);
int incr = t & 255; // an unknown increment 0..255
```

and then we could increment by `incr` instead of 1.

Unfortunately, the compiler is smart enough to see that the result is `kIterations * incr` and optimize it away.

To defeat dead code optimization, we could use this little hack to make the compiler unable to prove the deadness of `sum`:
```
bool nevertrue = (time(NULL) == 0);
if (nevertrue) {
 fprintf(..., sum); // this will never get called but sum is now live
}
```

## a better loop

We can force the compiler to perform the full loop by declaring `sum` or `increment` as `volatile`, meaning that its value may change at any time due to shared access by some other code.

This doesn't fix the problem of loop overhead, but it does keep the loop around.

To reduce the loop overhead, some unrolling can help. Unrolling four times reduces the effect of loop overhead by a factor of 4:

```
for (int i=0; i < kIterations; i+=4) {
  sum += i;
  sum += i;
  sum += i;
  sum += i;
}
```

To effectively eliminate loop overhead, time two different loops, one with $N_{1}$ and one with $N_{2}$ adds inside the loop; then you can subtract the two to get a good approximation of the time, with loop overhead cancelled out. Keep $N$ greater than 2, since the compiler may generate a different faster loop code for 0, 1, or 2.

## Dependent Variables

Imagine we change the previous sample to:

```
for (int i=0; i < kIterations; i+=4) {
  sum += i;
  sum2 += i;
  sum += i;
  sum2 += i;
}
```

Now when we measure this on a superscalar CPU we might get an average of 0.5 cycles for an add; we basically get `sum2` for free while `sum` is loading and executing.

To measure actual _latency_ instead of _issue rate_, we need to make sure that each measured instruction is dependent on the result of the previous one.

A compiler can reorder operations. Consider:

```
volatile uint64_t incr0 = ...;
uint64_t prod = 1;
for (int i=0; i < kIterations; i += 4) {
	prod *= incr0;
	prod *= incr1;
	prod *= incr2;
	prod *= incr3;
}
```
You might expect the compiler to do four dependent multiples:
`prod = (((prod * incr0) * incr1) * incr2) * incr3
but gcc -O2 rearranges that into:
```
temp = ((incr0) * incr1) * incr2) * incr3;
prod = prod * temp;
```

now `temp` is a loop constant, and the CPU can effectively do four operations at once.

(I think I'm missing a bit when they say:
> With multi-issue and instruction pipelining, the sample server CPU hardware can in fact keep at least four iterations of the loop in flight at once, with the multiples overlapped

but I'm just going to carry on)

## More nuance

To turn off this optimization you can use `-fno-tree-reassoc`

consider the actual values that participate in your measurements - some might be especially fast or implemented in non-representative ways. Adding 0, multiplying by 1 or 0, all might be special-cased. Overflowing or underflowing may cause slower code paths to come into usage.

## exercises

In the books' source code (see [[_meta]]) there is a mystery1.cc source file, which includes a header file `timecounters.h`, which has an appropriate aarch64 counterpart to `__rdtsc()`:

```
#elif IsRPi4_64
  // Increments once per 27.778 cycles for RPi4-B at 54 MHz counter and 1.5GHz CPU clock
  // Call it 28 cycles
  uint64_t counter_value;
  asm volatile("mrs %x0, cntvct_el0" : "=r"(counter_value));
  return counter_value * 28;
```

The author has specified its use on an Rpi4-b; here's an example of its use [in the real world](https://cs.github.com/tensorflow/tensorflow/blob/21cb15b81af8a96a9a84f021d17f80e813022a69/tensorflow/core/platform/profile_utils/cpu_utils.h#L76) in tensorflow:
```
#elif defined(__aarch64__)
    // System timer of ARMv8 runs at a different frequency than the CPU's.
    // The frequency is fixed, typically in the range 1-50MHz.  It can because
    // read at CNTFRQ special register.  We assume the OS has set up
    // the virtual timer properly.
    uint64_t virtual_timer_value;
    asm volatile("mrs %0, cntvct_el0" : "=r"(virtual_timer_value));
    return virtual_timer_value;
```

I tested that my m1 mac hits the `IsRPi4_64` branch, but I assume that the exact frequency is probably not the same as RPi4-b, but probably this works fine anyway?

on my computer `gcc-11` is actual gcc provided by homebrew and `gcc` is symlinked to `clang` by mac, which is a dirty trick imo, but is what it is.

That header file also has a `__pause` instruction, which doesn't have an `aarch64` equivalent listed, but some quick investigation suggests that `yield` might be the equivalent? The author uses the gcc intrinsic version of pause, but this example [from boost](https://cs.github.com/phusion/passenger/blob/9640816af708867d0994bd2eddb80ac24399f855/src/cxx_supportlib/vendor-modified/boost/atomic/detail/pause.hpp?q=aarch64+yield+pause#L47-L51) uses asm for both branches:

```
#if defined(__i386__) || defined(__x86_64__)
    __asm__ __volatile__("pause;" : : : "memory");
#elif (defined(__ARM_ARCH) && __ARM_ARCH >= 8) || defined(__ARM_ARCH_8A__) || defined(__aarch64__)
    __asm__ __volatile__("yield;" : : : "memory");
#endif
```

This won't be necessary in this chapter, but may become useful later.

### 2.2

> compile and run `mystery1.cc` both unoptimized -O0 and optimized -O2. Explain the differences
```
$ ./mac-mystery ; echo "-----"; ./mac-mystery-o2
1000000000 iterations, 1402525936 cycles, 1.40 cycles/iteration
-----
1000000000 iterations, 0 cycles, 0.00 cycles/iteration
```

Obviously gcc eliminates the loop on O2.

### 2.3

The author left in a commented-out fprint line to make the sum live, but gcc still eliminates the loop on O2 with it uncommented. My guess is that the compiler is still able to optimize out the loop by figuring out that it's `incr * kIterations`?

### 2.4

Marking it volatile gets us more than zero cycles:

```
$ gcc-11 -o mac-mystery-o2-volatile -O2 mystery1.cc; ./mac-mystery-o2-volatile
1000000000 iterations, 264643092 cycles, 0.26 cycles/iteration
1644937006 46000000000
```

but still shows us an impossible 0.26 cycles/it (mac) and a more reasonable 2.36 cycles/it (linux/docker).

My guess is that the mac is doing some sort of simultaneous execution? But I don't know how to explain it exactly, would love to understand in more detail.

### 2.5

Make your own copy of mystery1.cc and give a reasonable measurement of the latency of cycles in a 64-bit add.

Already done, see above; but very confused why I'm getting a quarter of a cycle!

My guess is that a 64-bit add is one cycle on an ARM computer, but I'm really struggling for ideas on how to demonstrate that.

### 2.6

Experiment with some loop values in mystery1.cc - 1, 10, 100... 1,000,000,000. Explain why some values do not produce meaningful results

```
1          iterations, 0          cycles, 0.00 cycles/iteration
10         iterations, 28         cycles, 2.80 cycles/iteration
100        iterations, 84         cycles, 0.84 cycles/iteration
1000       iterations, 588        cycles, 0.59 cycles/iteration
10000      iterations, 5376       cycles, 0.54 cycles/iteration
100000     iterations, 53368      cycles, 0.53 cycles/iteration
1000000    iterations, 532952     cycles, 0.53 cycles/iteration
10000000   iterations, 5349176    cycles, 0.53 cycles/iteration
100000000  iterations, 40507040   cycles, 0.41 cycles/iteration
1000000000 iterations, 366967076  cycles, 0.37 cycles/iteration
```

For 1 iteration, we can guess that it was just too fast for the sample rate of the timer. For 10 and 100 iterations, we can guess that the same cause will give us pretty widely varying answers, depending on sample timing.

After that, we settle pretty quickly down to 1/3 to 1/2 of a cycle.

A thought: I'm using the timer frequency calculation given by the author for an RPi 4, but actually I'd assume it's different on my mac? Also I've discovered that there are two timers on ARM:

> The 'virtual counter' is an architectural concept in the Arm
architecture, not a virtual (in the software VM sense) counter.

> The Arm Generic Timer Architecture defines two counters:
 - The physical counter, accessed via CNTPCT_EL0
 - The virtual counter, accessed via CNTVCT_EL0

> And a number of timers.  All timers are associated with the physical
counter, except the 'EL1 Virtual Timer' which uses the count in the
virtual counter for its comparison.

> The virtual counter yields the value of the physical counter minus an
offset.

> That offset is controlled by a hypervisor running at EL2 which can
program the offset value in CNTVOFF_EL2.

> The basic idea is that a VM can use the virtual timer/counter to keep
track of some notion of virtual time, and the physical timer/counter to
keep track of something that always relates to wall-clock time.

- https://lists.cs.columbia.edu/pipermail/kvmarm/2018-November/033143.html

The Mac m1 wiki page says that my computer's max CPU freq is 3.2; a search shows:

> The Apple M1 Max is a System on a Chip (SoC) from Apple that is found in the late 2021 MacBook Pro 14 and 16-inch models. It offers all 10 cores available in the chip divided in eight performance cores (P-cores with **600 - 3220 MHz**) and two power-efficiency cores (E-cores with 600 - 2064 MHz)

And we can get the current frequency with this command (I'm currently on battery):

```
$ sudo /usr/bin/powermetrics -s cpu_power -n 1 | grep CPU.*freq
CPU 0 frequency: 1247 MHz
CPU 1 frequency: 1249 MHz
CPU 2 frequency: 1153 MHz
CPU 3 frequency: 1302 MHz
CPU 4 frequency: 1558 MHz
CPU 5 frequency: 1188 MHz
CPU 6 frequency: 1272 MHz
CPU 7 frequency: 1569 MHz
CPU 8 frequency: 1528 MHz
CPU 9 frequency: 1295 MHz
```

So what the fuck am I supposed to do with this? I have no idea what the CPU frequency of the core I'm actually running the code on is - it could be anywhere from 600 Mhz to 3220Mhz.

Well, let's just guess for now maybe that it will be ~1500mhz? Given that we have a counter with 24,000,000 = 24mhz resolution, we could estimate 1500/24 = 62.5 cycles per timer increment.

Unfortunately, that still gets us <1 cycle per instruction.

It's possible that `DWT_CYCCOUNT` might work? but I haven't played with it at all and documentation is thin on the ground.

https://stackoverflow.com/questions/64475200/stm32-dwt-cycle-counter-cyccnt-surprising-behavior-rust

https://developer.arm.com/documentation/ddi0403/d/Debug-Architecture/ARMv7-M-Debug/The-Data-Watchpoint-and-Trace-unit/CYCCNT-cycle-counter-and-related-timers?lang=en

A random article [I found on the web](https://dougallj.wordpress.com/2022/08/20/faster-zlib-deflate-decompression-on-the-apple-m1-and-x86/) by somebody who seems to know what thy're doing says:

> The M1 can run 8 instructions per cycle, meaning that we have time to run 64 instructions during that 8-cycle latency chain

So maybe the .24 I was seeing earlier was actually correct?