as3redtamarin
=============

The Redtamarin command-line tool.

You have Redtamarin "the project" which produce
the different Redtamrin shells or `redshell`

And now you have `redtamarin`, a tool that allows to 
run ActionScript 3.0 on the command-line easily.

Usage
-----

```bash
redtamarin - Run ActionScript 3.0 on the command-line.

Usage: 
-h, --help        Print this usage information.
-v, --version     Print Redtamarin version.
    --debug       Run redshell debug.
    --debugger    Run redshell debugger.
```

Why ?
-----

Because we can :).

More seriously, here are the improvements
  - simpler, cleaner, more user-friendly
  - run faster than a Bash shell script
  - remove the need to use "--"
  - allow to pass arguments with spaces
  - (more features to come)


What's the Difference ?
-----------------------

Let's say you want to execute an ABC file with the Redtamarin Debugger Shell
and pass some arguments to it, you would do:  
`$ redshell_dd program.abc -- a b c`

With redtamarin utility it is bit easier:  
`$ redtamarin --debugger program.abc a b c`


Let's say you want to know which version of Redtamarin is installed,
with the Redtamarin Debugger Shell you would do:  
`$ redshell_dd -Dversion`

and obtain:
```bash
shell 2.1 debug-debugger build cyclone
Description: redtamarin-0.4.1.1T180-beta
features AVMSYSTEM_64BIT;AVMSYSTEM_UNALIGNED_INT_ACCESS;
AVMSYSTEM_UNALIGNED_FP_ACCESS;AVMSYSTEM_LITTLE_ENDIAN;
AVMSYSTEM_AMD64;AVMSYSTEM_MAC;AVMFEATURE_DEBUGGER;
AVMFEATURE_ALLOCATION_SAMPLER;AVMFEATURE_JIT;AVMFEATURE_COMPILEPOLICY;
AVMFEATURE_ABC_INTERP;AVMFEATURE_SELFTEST;AVMFEATURE_EVAL;
AVMFEATURE_PROTECT_JITMEM;AVMFEATURE_SHARED_GCHEAP;
AVMFEATURE_MEMORY_PROFILER;AVMFEATURE_CACHE_GQCN;AVMFEATURE_SAFEPOINTS;
AVMFEATURE_INTERRUPT_SAFEPOINT_POLL;AVMFEATURE_SWF12;AVMFEATURE_SWF13;
AVMFEATURE_SWF14;AVMFEATURE_SWF15;AVMFEATURE_SWF16;AVMFEATURE_SWF17;
AVMFEATURE_SWF18;AVMFEATURE_SWF19;AVMTWEAK_EXACT_TRACING;
```
a bit overcrowded don't you think?

With redtamarin utility you do:  
`$ redtamarin -v`

and obtain:  
```bash
0.4.1
```
it is cleaner and simpler


Details
-------

The Redtamarin Shells are powerful tools but they have been originally
made to debug the AVM2 (ActionScript Virtual Machine) and so contain
a hell lot of options and even extremely advanced options.

> **Yoda:** Scared? You will be...

This could have been solved in numerous ways, for example we were using
Bash shell scripts (see [an example here](https://gist.github.com/zwetan/97cf1838f4d3d72bbc93)),
but really it was not ideal as you would end up with a chain of symlink:  
`/usr/bin/redshell -> /usr/lib/redtamarin/bin/redshell -> /usr/lib/redtamarin/runtimes/linux/64/redshell`

And then on our last update `0.4.1` we made some change which allowed us
to simply reuse our own dog food to solve our own problems.

The `redtamarin` executable provide clearer and cleaner command-line options,
but also use a native system call to launch the `redshell` executables:  
from `C.unistd.*` we use `execv()` and so instead of redirecting a process
we are directly replacing the process in-memory and are able to control
how/where we are calling it, its environment variables and command-line arguments.

TODO


