# [EDR](https://github.com/cutepig123/gitblog/issues/43)

安全攻防之wmi

# 进攻

## wmi能干啥



## 怎样用wmi

### pyhton wmi

https://www.cnblogs.com/mingerlcm/p/10498530.html

http://timgolden.me.uk/python/wmi/tutorial.html

```python
pip install wmi  
pip install pypiwin32  

import win32con
import wmi

w = wmi.WMI()
cpu_list = w.Win32_Processor()
print(cpu_list)
# [<_wmi_object: b'\\\\QH-20181120YSCF\\root\\cimv2:Win32_Processor.DeviceID="CPU0"'>]

disk = w.Win32_DiskDrive()[0]
print(disk)

w.Win32_NetworkAdapterConfiguration()

self.obj=wmiobj.Win32_OperatingSystem()[0]  
self.obj.Win32Shutdown()
self.obj.Reboot()
self.obj.Shutdown()

# service
self.obj=wmiobj.Win32_Service(Name=self.name)[0]    #obj in the list

# process
c.Win32_Process??
p.GetOwner()	
p.Terminate()
c = wmi.WMI()
>>> import win32con
>>> startup = c.Win32_ProcessStartup.new(ShowWindow=win32con.SW_SHOWMAXIMIZED)
>>> pid, retval = c.Win32_Process.Create(CommandLine="notepad.exe",ProcessStartupInformation=startup)

c.Win32_UserAccount
c.Win32_GroupUser
users, total, uresume = win32net.NetLocalGroupGetMembers (None, 'Administrators', 0, uresume)
            for sid in (u['sid'] for u in users):
                username, domain, type = win32security.LookupAccountSid (None, sid)
                admin_list.append(username)
                
# who ami
a=c.query('SELECT UserName FROM Win32_ComputerSystem')
>>> a[0].UserName
'HJS-PC\\cutepig'

>>> c._getAttributeNames()
['Win32_PNPAllocatedResource', 'Win32_VolumeQuotaSetting', 'MSFT_NetServiceNotInteractive', 'CIM_ReplacementSet', 'Win32_ThreadStartTrace', 'Win32_DiskPartition', 'Msft_WmiProvider_GetObjectAsyncEvent_Post', 'MSFT_NetServiceSlowStartup', 'Win32_PerfFormattedData_Counters_PacketDirectReceiveCounters',...
 

```

https://cloud.tencent.com/developer/article/1568596

```python
# -*- coding:utf-8 -*-

import datetime
import os
import wmi
import time
import _winreg
import pythoncom
import threading
import win32api
import win32con
import Queue
c = wmi.WMI()

# 如果要连接远程机器，只需要在WMI构造器中指定远程机器名即可
# c = wmi.WMI("some_other_machine")

# List All Running Processes 
# 列出所有正在运行的进程
for process in c.Win32_Process():
	print process.ProcessID,process.Name

# List All Running Notepad Processes
# 列出所有正在运行的记事本进程 
for process in c.Win32_Process(name="notepad.exe"):
	print process.ProcessID,process.Name

# Create And Then Destroy A New Notepad Process
# 创建一个新的记事本进程然后结束它
process_id, return_value = c.Win32_Process.Create(CommandLine="notepad.exe")
for process in c.Win32_Process(ProcessId=process_id):
	print process.ProcessID, process.Name

result = process.Terminate()

# Show The Interface For The .Create Method Of A Win32_Process Class
# 显示Win32_Process类的.Create方法的接口 
# 注：wmi模块会接受WMI方法的传入参数作为Python的关键字参数，并把传出参数作为一个元组进行返回。
print c.Win32_Process.Create

# Show All Automatic Servieces Which Are Not Running
# 显示没有处于正常运行状态的自启动服务
stopped_services = c.Win32_Service(StartMode="Auto", State="Stopped")
if stopped_services:
	for s in stopped_services:
		print s.Caption, "service is not running"
else:
	print "No auto service stopped"

# Show The Percentage Free Space For Each Fixed Disk
# 显示每个固定磁盘的剩余空间百分比
for disk in c.Win32_LogicalDisk(DriveType=3):
	print disk.Caption, "%0.2f%% free" % (100.0 * long(disk.FreeSpace) / long(disk.Size) )

# Run Notepad, Wait Until It's Closed And Then Show Its Text
# 运行记事本，等它关闭之后显示它里面的文字 
# 注：这个例子是运行一个进程并且知道它什么时候结束，而不是去处理输入到记事本里面的文字。\
# 所以我们只是简单的用记事本打开一个指定文件，等到用户完成输入并关闭记事本之后，显示一下它的内容。 
filename = r'E:\Tools\test.txt'
process = c.Win32_Process
process_id, result = process.Create(CommandLine="notepad.exe " + filename)
watcher = c.watch_for(
	notification_type = "Deletion",
	wmi_class = "Win32_Process",
	delay_secs = 1,
	ProcessId = process_id
	)

watcher()
print "This is what you wrote:"
print open(filename).read()

# Watch For New Print Jobs
# 监视新的打印任务
print_job_watcher = c.Win32_PrintJob.watch_for(
	notification_type = "Creation",
	delay_secs = 1
	)

while 1:
	pj = print_job_watcher()
	print "User %s has submitted %d pages to printer %s" % \
	(pj.Owner, pj.TotalPage, pj.Name)

# Reboot A Remote Machine
# 重启远程机器
# 注：要对远程系统进行这样的操作，WMI脚本必须具有远程关机(RemoteShutdown)的权限，\
# 也就是说你必须在连接别名中进行指定。WMI构造器允许你传入一个完整的别名，或者是指定你需要的那一部分。\
# 使用wmi.WMI.__init__的帮助文档可以找到更多相关内容。
# other_machine = "machine name of your choice"
d = wmi.WMI(computer=other_machine, privileges=["RemoteShutdown"])

os = d.Win32_OperatingSystem(Primary=1)[0]
os.Reboot()


# Show the IP and MAC addresses for IP-enabled network interfaces
# 对于启用IP的网卡显示其IP和MAC地址
for interface in c.Win32_NetWorkAdapterConfiguration(IPEnabled=1):
	print interface.Description, interface.MACAddress
	for ip_address in interface.IPAddress:
		print ip_address
	print 


# What’s running on startup and from where?
# 查看自启动项
for s in c.Win32_StartupCommand():
	print "[%s] %s <%s> " % (s.Location, s.Caption, s.Command) 


# Watch for errors in the event log
# 监视事件日志中的错误信息
e = wmi.WMI(privileges=["Security"])

watcher = e.watch_for(
	notification_type = "Creation",
	wmi_class = "Win32_NTLogEvent",
	Type = "error"
	)

while 1:
	error = watcher()
	print "Error in %s log: %s " % (error.Logfile, error.Message)
	# send mail to sysadmin etc.

# List registry keys
# 列出注册表子键
# 注：本例及以下几例使用了Registry()这个方便的函数，此函数是早期加入到wmi包的，它等效于：
r = wmi.WMI(namespace="DEFAULT").StdRegProv
print r

r = wmi.Registry()
result, names = r.EnumKey(
	hDefKey = _winreg.HKEY_LOCAL_MACHINE,
	sSubKeyName = "Software"
	)

for key in names:
	print key

# Add a new registry key
# # 增加一个新的注册表子键
r = wmi.Registry()
result, = r.CreateKey(
	hDefKey = _winreg.HKEY_LOCAL_MACHINE,
	sSubKeyName = r"Software\TJG"
	)


# Add a new registry value
# 增加一个新的注册表键值
r = wmi.Registry()
result, = r.SetStringValue(
	hDefKey = _winreg.HKEY_LOCAL_MACHINE,
	sSubKeyName = r"Software\TJG",
	sValueName = "ApplicationName",
	sValue = "TJG APP"
	)

# Create a new IIS site
# # 创建一个新的IIS站点
k = wmi.WMI(namespace="MicrosoftIISv2")

#
# Could as well be achieved by doing:
#  web_server = c.IISWebService(Name="W3SVC")[0]
#

for web_server in k.IIsWebService(Name="W3SVC"):
	break

binding = k.new("ServerBinding")
binding.IP = ""
binding.Port = "8383"
binding.Hostname = ""
result, = web_server.CreateNewSite(
	PathOfRootVirtualDir = r"C:\inetpub\wwwroot",
	ServerComment = "My Web Site",
	ServerBinding = [binding.ole_object]
	)

# Show shared drives
# 显示共享目录

for share in c.Win32_Share():
	print share.Name, share.Path


# Show print jobs 
# 显示打印任务

for printer in c.Win32_Printer():
	print printer.Caption
	for job in c.Win32_PrintJob(DriverName=printer.DriverName):
		print " ", job.Document
	print 

# Show disk partitions
# 显示磁盘分区
for physical_disk in c.Win32_DiskDrive():
	for partition in physical_disk.associators("Win32_DiskDriveToDiskPartition"):
		for logic_disk in partition.associators("Win32_LogicalDiskToPartition"):
			print physical_disk.Caption, partition.Caption, logic_disk.Caption

# Install a product
# 安装一个产品

c.Win32_Product.Install(
	PackageLocation = 'E:\study\Python\python-2.7.8.msi',
	AllUsers = False
	)

# Connect to another machine as a named user
# 使用指定用户名连接另一台机器
# 注：你不能使用这个方法连接本机

#
# Using wmi module before 1.0rc3
#
connection = wmi.connect_server(
  server="other_machine",
  user="tim",
  password="secret"
)
n = wmi.WMI(wmi=connection)
 
#
# Using wmi module at least 1.0rc3
#
n = wmi.WMI(
  computer="other_machine",
  user="tim",
  password="secret"
)

# Show a method’s signature
# 显示一个方法的签名

for opsys in c.Win32_OperatingSystem():
	break

print opsys.Reboot
print opsys.Shutdown


# Schedule a job
# 创建任务计划
# 注：WMI的ScheduledJob类相当于Windows的AT服务(通过at命令来控制)。

one_minute_time = datetime.datetime.now() + datetime.timedelta(minutes=1)
job_id, result = c.Win32_ScheduledJob.Create(
	Command=r"cmd.exe /c dir /b c:\ > c:\\temp.txt",
	StartTime=wmi.from_time(one_minute_time)
	)

print job_id

for line in os.popen("at"):
	print line


# Run a process minimised
# 最小化的方式运行一个进程

SW_SHOWNMINIMIZED = 1
startup = c.Win32_ProcessStartup.new(ShowWindow=SW_SHOWNMINIMIZED)
pid, result = c.Win32_Process.Create(
	CommandLine="notepad.exe",
	ProcessStartupInformation=startup
	)
print pid


# Find Drive Types
# 查看磁盘类型

DRIVE_TYPE = {
	0 : "Unkown",
	1 : "No Root Directory",
	2 : "Removable Disk",
	3 : "Local Disk",
	4 : "Network Drive",
	5 : "Compact Disc",
	6 : "RAM Disk"
}

for drive in c.Win32_LogicalDisk():
	print drive.Caption, DRIVE_TYPE[drive.DriveType]


# List Namespaces
# 列出命名空间

def enumerate_namespaces(namespace = u"root", level=0):
	print level * " ", namespace.split("/")[-1]
	c = wmi.WMI(namespace = namespace)
	for subnamespace in c.__NAMESPACE():
		enumerate_namespaces(namespace + "/" + subnamespace.Name, level + 1)

enumerate_namespaces()

# Use WMI in a thread
# 在线程中使用WMI 
# 注：WMI技术是基于COM的，要想在线程中使用它，你必须初始化COM的线程模式，就算你要访问一个隐式线程化的服务也是如此。
 
class Info(threading.Thread):
    def __init__(self):
    	threading.Thread.__init__(self)
    def run(self):
    	print 'In Another Thread...'
    	pythoncom.CoInitialize()
    	try:
      		c = wmi.WMI()
      		for i in range(5):
        		for process in c.Win32_Process():
          			print process.ProcessId, process.Name
        		time.sleep(2)
    	finally:
      		pythoncom.CoUninitialize()
 
if __name__ == '__main__':
  	print 'In Main Thread'
  	c = wmi.WMI()
  	for process in c.Win32_Process():
  		print process.ProcessId, process.Name
  	Info().start()


# Monitor multiple machines for power events
# 监控多台机器的电源事件 
class Server(threading.Thread):

	def __init__(self, results, server, user, password):

		threading.Thread.__init__(self)
		self.results = results
		self.server = server
		self.user = user
		self.password = password
		self.setDaemon(True)

	def run(self):
		pythoncom.CoInitialize()
		try:
			#
		    # If you don't want to use explicit logons, remove
		    # the user= and password= params here and ensure
		    # that the user running *this* script has sufficient
		    # privs on the remote machines.
		    #
		    c = wmi.WMI(self.server, user = self.user, password = self.password)
		    power_watcher = c.Win32_PowerManagementEvent.watch_for()
		    while 1:
		    	self.results.put((self.server, power_watcher()))
		finally:
			pythoncom.CoUninitialize()

#
# Obviously, change these to match the machines
# in your network which probably won't be named
# after Harry Potter characters. And which hopefully
# use a less obvious admin password.
#

servers = [
	("goyle", "administator", "secret"),
	("malfoy", "administator", "secret")
	]

if __name__ == "__main__":
	power_events = Queue.Queue()
	for server, user, password in servers:
		print "Watching for", server
		Server(power_events, server, user, password).start()

	while 1:
		server, power_events = power_events.get()
		print server, "==>", power_events.EventType


# Find the current wallpaper
# 查看当前的墙纸

full_username = win32api.GetUserNameEx(win32con.NameSamCompatible)
for desktop in c.Win32_Desktop(Name = full_username):
	print desktop
	print \
		desktop.Wallpaper or "[No wallpaper]", \
		desktop.WallpaperStretched, desktop.WallpaperTiled
```



### wmi-client-wrapper

```python
pip install wmi-client-wrapper
import wmi_client_wrapper as wmi
wmic = wmi.WmiClientWrapper(username="localaccount",password="localpassword",host="<HostNameOrIpAddress>",)
output = wmic.query("SELECT * FROM Win32_Processor")
print(output)


```



https://segmentfault.com/a/1190000021661055

### 如何使远程进程可见？

https://devblogs.microsoft.com/scripting/how-can-i-remotely-start-an-interactive-process/

### wmic

```
/node::@c:\computers.txt product call install true,",c:\PathToYour\File.msi
```

### wmic

```
wmic /node:server process call create "cmd /C \"C:\\Program Files\\Mozilla Firefox\\firefox.exe\""
```



# 防守

## vbscript, python wmi crowdstrike

https://www.crowdstrike.com/blog/blocking-fileless-script-based-attacks-using-falcon-script-control-feature/

使用 CrowdStrike Falcon® 的脚本控制功能阻止基于无文件脚本的攻击

怀疑它可能是

- 使用了API hook技术，hook所有WMI COm接口操作，然后反向看看是哪个进程做的。这样的缺点是如果用户再更底层做，他就不知道了
- 在驱动层次做api hook，直接截获系统调用。但这个是未公开资料，有风险



https://www.crowdstrike.com/blog/how-crowdstrike-uses-similarity-search-to-detect-script-based-malware-attacks/

一旦拿到脚本，他就可以用AI来分析是否恶意脚本

https://www.crowdstrike.com/blog/how-to-detect-and-prevent-impackets-wmiexec/

本王讲解他们是如何应对wmiexec 的

在寻找 wmiexec 时，防御者应该寻找 WMI 的使用情况。  防御者的第一步应该是分析涉及父进程的进程关系，称为 `WMIPRVSE.EXE`。  可疑进程，例如 `CMD.EXE`或者 `POWERSHELL.EXE`作为子进程运行 `WMIPRVSE.EXE`是一个危险信号

## Kernel attack

crowdstrike how does it blocks driver level

https://www.crowdstrike.com/blog/how-to-detect-and-prevent-kernel-attacks-with-crowdstrike/

他没明确说，但我感觉他是依赖驱动的漏洞数据库，通过检测驱动版本是否在它的列表里面



驱动层面截获进程创建

https://cloud.tencent.com/developer/article/1079508?areaSource=106002.19

　　PsSetCreateProcessNotifyRoutineEx

## chanpin EDR

**Falcon Prevent for Home Use** 

CrowdStrike 的競爭對手包括 **Cybereason、Tanium、RiskIQ、Cylance 和 Avecto**.

  **十大端點檢測與響應 (EDR) 軟件**  

-    賽網360。  
-    MVISION 端點安全。  
-    用於終結點的 Microsoft Defender。  
-    獵人。  
-    自適應防禦 360 / WatchGuard EPDR。  
-    人群安全。  
-    皮質 XDR。  
-    FireEye 端點安全。  