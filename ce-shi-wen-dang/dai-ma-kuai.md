# 代码块



`inline code` `内嵌代码`



```
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```

**Highlight:**

<pre class="language-scss"><code class="lang-scss">:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
<strong>}
</strong></code></pre>

C语言代码：

```c
struct semaphore
{
    int value;
    PCB *queue;
}
P(semaphore s)
{
    s.value--;
    if(s.value<0)
        sleep_on(s.queue);
}
V(semaphore s)
{
    s.value++;
    if(s.value<=0)
        wake_up(s.queue);
}
```

C++代码：

```cpp
#include <ros/ros.h>
#include <ros_industrial_learn/PathPosition.h>//包含自动生成的 自定义消息头文件
#include <stdlib.h>                           //标准库 产生rand()随机数

int main(int argc, char* argv[])
{
  ros::init(argc, argv, "PathPosition_pub_node");// 节点初始化
  ros::NodeHandle node;//创建节点句柄 给节点权限
  ros::Publisher pub = node.advertise<ros_industrial_learn::PathPosition>("position", 1000);//发布消息 队列大小
  ros_industrial_learn::PathPosition pp_msg;
  ros::Rate loop_rate (1);    //发布频率   控制 消息发布 频率   这个对象控制循环运行速度
  while(ros::ok()) 
  {
    srand(time(0)) ; 
    pp_msg.header.stamp = ros::Time::now();//时间戳
    float angle =   float(rand())  /  RAND_MAX  * 180 ;        //角度  为 0 到 180 之间的某个值
    pp_msg.angle = angle * 3.141592 / 180.0;//角度 弧度制
    pp_msg.x = 100.0 * cos(pp_msg.angle);//水平位置
    pp_msg.y = 100.0 * sin(pp_msg.angle);//垂直位置
    pub.publish(pp_msg);
    //ros::spinOnce();//给一次控制权  发布消息不需要调用回调函数
    ROS_INFO("Published message %.1f, %.1f, %.1f", pp_msg.x, pp_msg.y, pp_msg.angle * 180.0 / 3.141592);
    loop_rate.sleep();//给节点运行权限（按照指定频率）
  }
  return 0;
}
```

x86汇编：

```nasm
_start:
	mov	ax,#BOOTSEG
	mov	ds,ax
	mov	ax,#INITSEG
	mov	es,ax
	mov	cx,#256
	sub	si,si
	sub	di,di
	rep
	movw
	jmpi	go,INITSEG
go:	mov	ax,cs
	mov	ds,ax
	mov	es,ax
! put stack at 0x9ff00.
	mov	ss,ax
	mov	sp,#0xFF00		! arbitrary value >>512
```

ARM 汇编：

```armasm
rt_hw_context_switch:
    ;/* set rt_thread_switch_interrupt_flag to 1 */
    ;/* 加载 &rt_thread_switch_interrupt_flag 到r2 */
    LDR     r2, =rt_thread_switch_interrupt_flag

    ;/* 加载 rt_thread_switch_interrupt_flag 到r3 */
    LDR     r3, [r2]
    CMP     r3, #1
    BEQ     _reswitch   /* flag=1 执行 */
    MOV     r3, #1
    STR     r3, [r2]

    LDR     r2, =rt_interrupt_from_thread   /* set rt_interrupt_from_thread */
    STR     r0, [r2]

_reswitch:
    ;/* 设置r2为rt_interrupt_to_thread地址 */
    LDR     r2, =rt_interrupt_to_thread 
    ;/* 存储r1的值到下一个线程栈sp的指针 */
    STR     r1, [r2]
    ;/* 触发PendSV异常，实现切换 */
    LDR r0, =NVIC_INT_CTRL              
    LDR r1, =NVIC_PENDSVSET
    STR r1, [r0]
    ;/* 子程序返回 */
    BX  LR
```
