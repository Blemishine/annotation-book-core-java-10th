#  Chapter 4: Networking   网络  

[跳转代码InetAddressTest](../src/main/v2ch04/inetAddress/InetAddressTest.java)

telnet 命令
	无法连接到`time-a.nist.gov`域名
	换成`time.nist.gov`就可以显示时间了
linux


	$ telnet time-a.nist.gov 13
	Trying 129.6.15.28...
	Connected to time-a-g.nist.gov.
	Escape character is '^]'.
	Connection closed by foreign host.

	

	$ telnet time.nist.gov 13
	Trying 132.163.97.1...
	Connected to ntp1.glb.nist.gov.
	Escape character is '^]'.
	
	58399 18-10-08 13:59:22 28 0 0 621.2 UTC(NIST) *
	Connection closed by foreign host.
	
win

	58399 18-10-08 14:03:53 28 0 0 827.5 UTC(NIST) *
	遗失对主机的连接。