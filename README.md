# eandroid
android learn


0001:关于System.exit
     System.exit(0)是将你的整个虚拟机里的内容都停掉了 ，而dispose()只是关闭这个窗口，但是并没有停止整个application。无论如何，内存都释放了！                            也就是说连JVM都关闭了，内存里根本不可能还有什么东西
     System.exit(0)是正常退出程序，而System.exit(1)或者说非0表示非正常退出程序
     System.exit(status)不管status为何值都会退出程序。和return 相比有以下不同点：return是回到上一层，而System.exit(status)是回到最上层
     
     另 如果是在第一个 Activity 调用 Process.killProcess 或 System.exit(0) 都会 kill 掉当前进程。
        如果不是在第一个 Activity 中调用，如 ActivityA 启动 ActivityB ，你在 ActivityB 中调用Process.killProcess 或 System.exit(0) 
            当前进程确实也被 kill 掉了，但 app 会重新启动，又创建了一个新的进程[可以pid校验之]
	    
	    
0002：关于Service
      针对onStartCommand之返回值
      return START_NOT_STICKY;//即便startService  没有手动执行stopService 其也会自动停止
      return START_STICKY;//不手动 自动重启，启动间隔1S左右 此时intent为null 主应用再启动时 同其二次启动之pid 
      return START_REDELIVER_INTENT;/不手动 自动重启，此时intent为最近一次传入之对象   启动间隔20S左右主应用再启动时 同其二次启动之pid 
