# Hi5a Robot Controller Function Manual - Task Daemon

{% hint style="warning" %}
The information provided in this product manual is the property of Hyundai Robotics.

It cannot be reproduced or redistributed in part or whole without written consent from Hyundai Robotics, and it cannot be provided to third parties or used for other purposes.



The manual is subject to change without prior notification.



**Copyright ⓒ 2023 by HD Hyundai Robotics**
{% endhint %}
# 1. Overview

{% hint style="info" %}
This feature is supported from V40.27-17 and later versions.
{% endhint %}

In general, the JOB program on the Hi5a controller runs only when in automatic mode or when `StepFWD` is pressed in manual mode.  

Sometimes, however, you have to run a JOB program in the background, even if it's not under these playback conditions.  
For example, if JOB has implemented a network service function that reports the current state of the controller to the outside, this JOB should always be running regardless of the playback conditions above.

The Task Daemon feature allows you to assign a specific JOB to the desired task and always run it regardless of the playback conditions.



{% hint style="info" %}

`Daemon` is a term that refers to a program that usually continues to perform in the background and primarily handles service requests from external systems.

{% endhint %}

{% hint style="warning" %}

The TaskDaemon feature has the following limitations;

- Step statements such as MOVE are ignored without errors. You can't move a robot or an additive-axes devices.

- Task 0 or tasks used in the multi-task feature does not allowed to be used as a daemon.

- Most of the etc. statements below do not work.

```python
CALLPR, RINT, RINTA, COWORK  GUNCHNG AXISCTRL SELPTNO , FILTER, BrakeCheck, BrakeTest, GasPTest, ServoFree, SoftXYZ, OnLTrack, ForceCtrl, SoftJoint, 
PLCTrack, Tunning, TOOLCHNG, SpeedCtrl, LoadEst, SEALER, UDPsnd, Tool, etc...
```

- Most of the robot application statements as below do not work.

```python
ARCON, LVSON, MULTPASS, RHemming, WaitSensor, HSensON, 등...
```

- If you edit a JOB running as TaskDaemon, you might stop running daemon for that task in some cases.

{% endhint %}
# 2. How to use
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
# 2.2. Monitoring

![Task daemon monitoring](../_assets/monitoring.png)


You can view the current program counters for the task daemon in the `[R2: Window adjustment] - [F1: Content selection] - 18: Multi-tasking state`
# 2.3. JOB editing

The main JOB programs or sub-JOB programs in the task daemon are freely editable. However, if you insert/delete a command statement or edit an IF statement when these programs are in the call stack (i.e., running), the following confirmation dialog box appears.

![Stop or reset confirmation dialog](../_assets/stop_reset_dialog.png)

Pressing the `[ENTER]` key stops and resets the task daemon. Press the `[ESC]` key to cancel the edit.

And, if you delete a JOB program in the call stack, its daemon execution is interrupted and initialized.
# Appendices

  # Rules on Occupational Safety and Health Standards, and Notice for Safety Inspection

The industrial robot should be installed in consideration of the inspection standards both of the Rules on Occupational Safety and Health Standards and of the Notice for Safety Inspection \(if subject to inspection\).

"[Rules on Occupational Safety and Health Standards](https://hrbook-hrc.web.app/#/view/rules-on-occupational-safety-and-health-standards/english/README)"
# Quality Assurance

"[Quality Assurance](https://hrbook-hrc.web.app/#/view/quality-assurance/english/README)"
