# Useful commands:

Command cheat sheet: https://lldb.llvm.org/lldb-gdb.html

`bt` - Show a current backtrace
`expr XXXX` - Run some code
`frame variable XXXXX` - Show information about that variable
                         e.g. (mozilla::profiler::AllocationTracker::AllocationSet *) mAllocations = 0x0000000000000000
`f` - List the source code of the current stack frame
`f 2` - List the source code of a previous stack frame
`l` - List source code
`l 300` - List source code from line 300
`s` - Step in
`n` - Next
`continue` - Continue running the program
`finish` - Step out of the currently selected frame.
`breakpoint set -f foo.c -l 12` - Set a breakpoint at a file and line number (didn't work)

## Debugging via mach run

* Do a debug build
* `mach run --debug`
* Set a breakpoint by:
  * `breakpoint set --name nsInProcessTabChildGlobal::InitTabChildGlobal`
  * `b nsInProcessTabChildGlobal::InitTabChildGlobal`
  * `b test.c:12`
  * Method name: `br s -M methodName`
  *
* From lldb's CLI, run: `r`, which is short for `run`.

## Connect to a content process:

 * Hover over a content tab, note the PID
 * From another terminal window run: `lldb -p PID`

## Connect to an xpc-shell test

 * `./mach xpcshell-test --debugger lldb --debugger-interactive $TEST_NAME`
 * Then run `process launch`

## Child process debugging

Run things with --disable-e10s
Spit out all the PIDs of: MOZ_DEBUG_CHILD_PROCESS=1

## Examples:

```bash
mach run --debug
# Set some breakpoints
b InitPoisonIOInterposer
b ProfilerIOInterposeObserver::Observe
b ActivePS::ActivePS
# Run the executable
r
# A breakpoint catches, start stepping
s
s
s
# Now inspect a frame variable

```

## Expressions

Show the result in binary:
`expr --format binary -- YOUR_EXPRESSION`
