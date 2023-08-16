﻿# 1. 개요

{% hint style="info" %}
이 기능은 V40.27-17 및 이후 버전부터 지원됩니다.
{% endhint %}

일반적으로 Hi5a 제어기의 JOB 프로그램은 자동모드일 때, 혹은 수동모드이면서 StepFWD를 누르고 있을 때만 수행됩니다.

그러나 때로는, 이러한 재생 조건이 아닐 때에도, 백그라운드에서 JOB프로그램을 실행해야 할 경우가 있습니다. 
가령, 제어기의 현재 상태를 외부로 보고하는 네트워크 서비스 기능을 JOB으로 구현했다면, 이 JOB은 위와 같은 재생 조건과 무관하게 항상 실행되고 있어야 유용할 것입니다.

태스크 데몬 (Task Daemon) 기능을 활용하여, 특정한 JOB을 원하는 태스크에 할당하고 이를 재생 조건과 무관하게 항상 실행할 수 있습니다.

{% hint style="info" %}
데몬 (daemon)이란, 보통 백그라운드에서 계속 수행되면서 주로 외부 시스템으로부터의 서비스 요청을 처리해주는 프로그램을 의미하는 용어입니다.
{% endhint %}

{% hint style="warning" %}

TaskDaemon 기능은 아래와 같은 제약이 있습니다.

- MOVE 등 스텝 명령문은 에러 없이 무시됩니다. 즉, 로봇이나 부가축 장치를 움직일 수는 없습니다.

- 태스크 0이나 멀티태스크 기능에 의해 사용 중인 태스크 번호는 데몬으로 사용할 수 없습니다.

- 아래와 같은 기타 명령문들은 대부분 동작하지 않습니다.

```python
CALLPR, RINT, RINTA, COWORK  GUNCHNG AXISCTRL SELPTNO , FILTER, BrakeCheck, BrakeTest, GasPTest, ServoFree, SoftXYZ, OnLTrack, ForceCtrl, SoftJoint, 
PLCTrack, Tunning, TOOLCHNG, SpeedCtrl, LoadEst, SEALER, UDPsnd, Tool, 등...
```

- 아래와 같은 로봇 응용 명령문들은 대부분 동작하지 않습니다.

```python
ARCON, LVSON, MULTPASS, RHemming, WaitSensor, HSensON, 등...
```

- TaskDaemon으로 실행 중인 JOB을 편집하면, 경우에 따라 해당 태스크의 daemon 실행은 정지할 수도 있습니다.

{% endhint %}
