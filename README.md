# ProtoThread-Core

 ProtoThread内核，从Contiki NG中提取而出，已经做好充分性移植准备工作，可以直接移植到单片机上。

 移植中只需关注pt_ports.c和pt_ports.h

 需要给protothread提供一个心跳时钟，将pt_ports.h注释中的几个函数语句放入中断中。

 定时器中断周期必须为pt_ports.h中 1s / PROTOTHREAD_CLOCK_SECONDS

 移植好的工程合集在：https://github.com/smartmx/ProtoThread-Templates





