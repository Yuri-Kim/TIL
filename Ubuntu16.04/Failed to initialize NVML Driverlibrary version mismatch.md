# Failed to initialize NVML: Driver/library version mismatch

GPU 사용중 아래와 같은 오류가 발생할 경우

~~~
Failed to initialize NVML: Driver/library version mismatch
~~~

nvidia driver를 unload 하고 관련 모듈을 삭제 (아래 명령어로 nvidia 관련 사용 드라이버 리스트 확인)

~~~
$ lsmod | grep nvidia

nvidia_uvm            634880  8
nvidia_drm             53248  0
nvidia_modeset        790528  1 nvidia_drm
nvidia              12312576  86 nvidia_modeset,nvidia_uvm
~~~

nvidia 드라이버 unload를 위하여 nvidia 항목 오른쪽에 있는 종속성 항목을 unload

~~~
$ sudo rmmod nvidia_drm
$ sudo rmmod nvidia_modeset
$ sudo rmmod nvidia_uvm
~~~

이 과정에서 "rmmod: ERROR: Module nvidia is in use" 와 같은 에러를 만나면 아래 명령어로 관련 프로세스 kill.

~~~
$ sudo lsof /dev/nvidia*
~~~

Reboot (Reboot 안해도 되는 경우도 있음)

~~~
$ reboot
~~~

nvidia driver kernel 이 정상적으로 로딩 되고 문제가 해결 되었는지 확인

~~~
$ nvidia-smi
~~~

