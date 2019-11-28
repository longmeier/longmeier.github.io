---
layout: post
title: "python操作串口文档"
author: "longmeier"
categories: journal
tags: [documentation,sample]
image: cutting.jpg
---

### 介绍
 pySerial
 封装了串口通讯模块，支持linux、windows、Bsd(可能支持所有支持POSIX的操作系统),支持Jython、IconPython

首页 http://pyserial.sf.net/
### 特性
#### 1. 所有平台使用同样的类接口
#### 2. 端口号默认从0开始，程序中不需要知道端口名称
#### 3. 像文件读写一样的API，read、write（readline等也受支持）

### 安装
 pip install pyserial
 
### 快速上手

#### 1. 实例化serial对象
 ```   
  try:
      ser = serial.Serial(port='com4', baudrate=9600, bytesize=serial.SEVENBITS, parity=serial.PARITY_ODD,
      stopbits=serial.STOPBITS_ONE)
      print('串口易打开...')
      loging('info', '串口已打开')
  except Exception as e:
      print('串口打开失败')
      loging('error', '串口打开失败error:%s' % str(e))
        
  * 注意：发送信息这是的是什么参数，接受的时候也设一样的参数进行接收，否则接收过来的数据无法解析。
 ```
#### 2.获取通讯数据
  ```
  while ser.isOpen():
      meta = dict()
      if (ser.in_waiting > 0):
          loging('info', '捕获信息....')
          buffer = ser.read(ser.in_waiting)
          print(buffer, str(type(buffer)))
          loging('info', str(buffer))
          print('捕获信息', str(buffer))
          result = buffer.decode()

      elif (ser.in_waiting <= 0):
          time.sleep(1)
          print('end...')
   ```
#### 3.serial 属性和方法
  ```
  open()                    # 打开端口

  close()                   # 立即关闭端口

  setBaudrate(baudrate)     # change baud rate on an open port

  inWaiting()               # return the number of chars in the receive buffer

  read(size=1)              # read “size” characters

  write(s)                  # 把字符串s写到该端口

  flushInput()              # 清除输入缓存区，放弃所有内容

  flushOutput()             # 清除输出缓冲区，放弃输出

  sendBreak()               # 发送中断条件

  setRTS(level=1)           # set RTS line to specified logic level

  setDTR(level=1)           # set DTR line to specified logic level

  getCTS()                  # return the state of the CTS line
  ```
#### 4.常量
  ```
  parity:

        serial.PARITY_NONE   serial.PARITY_EVEN  serial.PARITY_ODD

  stopbits：

        serial.STOPBITS_ONE   serial.STOPBITS_TWO

  bytesize:

        serial.FIVEBITS、serial.SIXBITS、serial.SEVENBITS、serial.EIGHTBITS
  ```