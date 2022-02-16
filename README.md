# ProtoThread-Core

## Protothread介绍

ProtoThread内核，从Contiki NG中提取而出，已经做好充分性移植准备工作，可以直接移植到单片机上。

## 移植

移植需要在pt_ports.h中修改配置

```c
typedef unsigned long                   clock_time_t; //定义时钟变量类型

#define PROCESS_CONF_NO_PROCESS_NAMES   1 //是否不存储process的名字，一般情况下没有必要存储，所以为1即可。

#define RINGBUF_INTERRUPT_SAFE_TYPE     uint16_t  //必须是系统中断安全的位数，决定了ringbuf的最大容量

#define PROTOTHREAD_CLOCK_SECONDS       1000  //根据提供的心跳时钟决定，比如1ms一次中断驱动，则该值为 1s / 1ms = 1000
```

然后在pt_ports.c中实现获取心跳时钟的函数

```c
/*********************************************************************
 * @fn      protothread_clock_init
 *
 * @brief   ProtoThread心跳时钟初始化，如果在外边自行实现了定时器初始化，则该函数可以为空
 *
 * @param   None.
 *
 * @return  None.
 */
void protothread_clock_init(void)
{

}

/*********************************************************************
 * @fn      protothread_clock_time
 *
 * @brief   获取心跳时钟的值
 *
 * @param   None.
 *
 * @return  clock_time_t 心跳时钟的值.
 */
clock_time_t protothread_clock_time(void)
{

}
```

如果使用protothread中软件定时器的功能，还需要实现etimer，  
定时器中断周期为pt_ports.h中 1s / PROTOTHREAD_CLOCK_SECONDS

```c
//移植需要在定时器中断中调用以下语句
if(etimer_pending() && etimer_next_expiration_time()<= ptTicks)
{
    etimer_request_poll();
}
```

## examples

移植好的工程合集在：[ProtoThread-Templates](https://blog.maxiang.vip/ProtoThread-Templates/)

## [博客主页](https://blog.maxiang.vip/)
