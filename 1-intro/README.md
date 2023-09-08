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
