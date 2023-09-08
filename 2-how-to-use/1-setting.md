# 2.1. Setting

Select `[F2: Systems] - 4: Application Parameters - 33: Task Daemon`.

![Task Daemon menuu](../_assets/menu.png)

<br>

The setup screen below opens.  
Settings are available for Task 1 ~ Task 7. (Task 0 cannot be used as a daemon.)

- When you enter a JOB number in the `JOB number` entry, the task is set to run as a daemon with that number as the main program.  
If set to 0, the task is not used as a daemon, i.e. the `daemon OFF` state.

- If you check `Auto.run`, the daemon will run automatically when you complete the setup or boot the controller.
- If you check `Repeat`, it will repeat from the beginning when JOB CYCLE is completed. This is the same concept as setting the `Condition setting - Operation Cycle` setting to `Continuous`.

- The `Status` item displays the current program counter (Program number/Step number/Function number) in parentheses, along with the current status of the task.

  - OFF: Not in use as a daemon.
  - OCCUPIED: A task occupied and in use by a multi-task function. Not available as daemon.
  - READY : The state of waiting to be STARTed on the program header.
  - RUN: The state of running as a daemon.
  - STOP : Running is stopped.
  - WAITING: Waiting by the DELAY, WAIT, or INPUT statement.
  - ERROR: An error has occurred. An error code may also be displayed.
  - END : JOB CYCLE is complete.

![Task daemon setting screen](../_assets/setting.png)

The F keys at the bottom allow manual operation of the task where the cursor is currently located.

- `[F1: Reset]` : Stops the selected task and performs a reset. It's the same concept as performing `R0[ENTER]`. All call information and local variables are cleared, and the program counter is placed on the main program header position.
- `[F2: Execute]` : Run the task daemon in the STOP, READY or END state. It's the same concept as pressing the `START` button.
- `[F3: Stop]` : Stops the task daemon in the RUN or WAITING state. It's the same concept as pressing the `STOP` button.

- `[F7: Complete]` : Save the settings and close the settings screen. The task daemon that you set to `Auto.run` starts running.
