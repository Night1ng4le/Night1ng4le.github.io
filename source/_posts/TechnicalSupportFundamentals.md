---
title: Technical Support Fundamentals
categories: [CS base]
tags: [google,IT,fundamentals]
---

### Intro to IT

- bits/bytes
- Computer Language/Character Encoding
	- ASCII -> UTF-8(Unicode)
	- ASCII只支持一个字节，UTF-8支持多字节编码
- Logic Gates
- Decimal forms(10-base)
- Abstraction
- Architecture Overview
	- Hardware
	- Operating System
	- Software
	- Users

<!--more-->

### Hardware
#### The Modern Computer
- **Computer**
	- calculate
	- process
	- store data
- **Ports**: Connection points that we can connect devices to that extend the functionality of our computer

- **Deep in Computer**
	- **CPU**(Center Process Units)
	- **RAM**(Random Access Memory, short-term memory)
	- **Hard drive**(holds all of our data, which includes all of our music, pictures, applications)
	- **Motherboard** 

- **Programs**
- CPU receive the bytes 
	- EDB(External data bus, with different sizes, 8 bit<8 wires>, 16 bit, 32 or 64...)
	- Registers
- CPU & RAM
```
          -------------
         |     RAM     |
          -------------
                |
                |
                |
          -------------    EDB      ----------
         |     MCC     |-----------|   CPU    |
          -------------             ----------
                |                        |
                 ------------------------
                       Address Bus


# MCC（Memory Control Chips）
# CPU通过Address BUS告知MCC自己需要的指令地址，MCC从RAM中取数据，通过EDB传送给CPU
```
- Cache：Cache存在CPU中，分为L1，L2，L3三级，L1是速度最快的。容量小于RAM，但速度比RAM更快。

- Clock Wire
	- 向CPU发送数据，则clock wire上会出现电压，提醒CPU开始上班～
	- Clock cycle - 时钟周期
	- Clock speed（一定时间内能执行的最大时钟周期数，例如3.4ghz = 3.4 billion cycle per second。这是理论上不能超越的值，真实情况未必能够达到）
	- overclocking(to increase CPU rate，常见于低端的CPU)

#### Components


- **CPU** 
	- instruction set(hard-coded in CPU)
	- different CPU manufactures may use different instruction set
	- eg: Intel、AMD、Qualcomm
	- 挑CPU的时候注意motherboard的兼容性

- **Major Sockets**
	- LGA(Land grid array) - 插脚突出
	- PGA(Pin grid array) - 插脚在处理器上
	- heat sink (避免overheating)

- **RAM**
	- volatile（断电即清空）
	- Program复制到RAM中给CPU运行
	- 16g RAM means it can run 16g program at the same time
	- DRAM(dynamic random-access memory)
	- DIMM(dual inline memory module)
	- SDRAM(synchronous DRAM)
	- DDR SDRAM(double data rate SDRAM)
		- faster
		- larger
		- need less power
		- have DDR1, DDR2, DDR3, DDR4(更快)

- **Motherboard** (it's a total boss)
	- Chip Set（manage data between CPU、RAM & peripherals[mouse、keyboard]）
		- Northbridge: interconnects RAM, video cards
		- Southbridge: 支撑I/O, hard drives, USB drives
	- Mordern Computer: 没有独立的北桥芯片

	- Expansion Slots
		- PCI Express(Peripheral Component Interconnect Express) 
			- PCIe bus(看起来像小型母板)
			- PCIe base expansion card(看起来像小型电路板)

	- Form Factor
		- ATX(Advanced Technology eXtended)
		- ITX(Information Technology eXtended)
			- mini-ITX
			- nano-ITX
			- pico-ITX
		- ITX比ATX小

- **Storage**
	- Data Sizes
		- A single byte can hold a letter, number or symbol
	- Hard Drive
		- HDD(Hard Disk Drives): 盘片+机械臂，更容易坏（活动部件多）
		- SSD(Solid State Drives): 快且更小但贵
		- RPM(revolution per minute)
	- Interface of Hard Drive
		- ATA Interfaces
		- Serial ATA Interfaces(SATA)可热交换(插电时可换)，使用cable传输
		- SATA满足不了SSD的需求，所以产生了NVMe(NVM Express)







#### Starting It Up


