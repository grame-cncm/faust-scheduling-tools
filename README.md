Faust Scheduling Test Suite
===========================

This test suite is a utility to test various scheduling strategies produced by the [Faust
compiler][1]. It is heavily inspired from [Faust Compiler Benchmark Tools][2].



Overview
--------

### Benchmarking

Benchmarking works by using [libpfm][3] to measure various CPU events over 1000 executions of your
DSP program's main loop. The use of libpfm means that currently, this benchmarking tool only works
on a Linux kernel.


To obtain a detailed plot of instructions and stalled cycles in all strategies compiled with
default settings, run :

```
fcschedtool plot <process.dsp>
```

This mode relies on Intel Skylake events that might not be available for your architecture.


To plot the evolution of a custom list of perf events, run :

```
fschedtool plot <process.dsp> -e perf_event[,other_perf_event]
```

Use `perf list` to get a list of perf events that work on your system.

Run `fcschedtool plot --help` for a detailed list of options.


### Testing

The testing feature works by sending an impulse in every input of a DSP and checking the response in
its outputs. The test passes if all scheduling strategies produce the same impulse response in every
output (within an acceptable floating-point margin of error).

To run tests on a given DSP, run :

```
fcschedtool test <process.dsp>
```


Examples
--------

The `dsp` folder contains a bunch of examples, taken from the [faust repository][4], that produce
particularly significant differences between the available scheduling policies.



[1]: https://github.com/grame-cncm/faust
[2]: https://github.com/grame-cncm/faustcompilerbenchtool
[3]: https://perfmon2.sourceforge.net/
[4]: https://github.com/grame-cncm/faust/tree/master-dev/examples

<!-- vim: set tw=100 -->
