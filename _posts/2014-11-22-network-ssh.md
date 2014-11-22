---
layout: default
title: linux.network.ssh
tags: linux network ssh
---
# 背景 # 
for getting the wisemapping open source,I do the next steps

# ssh.密钥 #
ssh-keygen -t dsa or >ssh-keygen -t rsa

> 1. ~/.ssh/id_dsa.pub --> this is the public key for the server which you ssh user@
> 2. ~/.ssh/id_dsa --> this is my private key

# ssh.client #

>chmod 600 ~/.ssh
>chmod 600 ~/.ssh/id_dsa.pub
>chmod 600 ~/.ssh/id_dsa

for logining the server you should add the host to you know_hosts
cat .ssh/known_hosts | grep wisemapping

# ssh.server #
login the wisemapping with the account the wise send to me

> I just copy the ~/.ssh/id_dsa.pub content to the website.
> copy and pasted the contents of the .pub on server2 in the 
> user's ~/.ssh/authorized_keys file and chmodded it 600.

# 登录服务器 #
>ssh -I ~/.ssh/id_dsa repo.wisemapping.org

	no support for smartcards.
	The authenticity of host 'repo.wisemapping.org (192.241.203.149)' can't be established.
	RSA key fingerprint is 42:da:87:96:63:09:b5:fd:4e:72:53:ce:78:95:31:dc.
	Are you sure you want to continue connecting (yes/no)? yes
	Failed to add the host to the list of known hosts (/home/limix/.ssh/known_hosts)
	limix@repo.wisemapping.org's password:

Failed to add the host to the list of known hosts (/home/limix/.ssh/known_hosts)


	ssh -I ~/.ssh/id_dsa repo.wisemapping.org                                                                                                  
	no support for smartcards.
	limix@repo.wisemapping.org's password:


So I search the RHEL no support for smart cards

	https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/enabling-smart-card-login.html
	Smart card login for *Red Hat Enterprise Linux servers* and *workstations* is not enabled by default and must be enabled in the system settings. 
	Using single sign-on when logging into Red Hat Enterprise Linux requires these packages: 
	*But this is for login into the redhat enterprise linux system not for log in the server I am processed.*

----
TRY the github to add my ssh public, and do my work*

	It works fine, so I don't know why it dones't work on some other system, 
	maybe the message no support for smartcards is from remote system, but i get 
	the same message in localhost. refer to the RHEL referrence linux not support 
	smart cards now, so it will give such a message.

	github 24king
	I create the user name 24king coollimix@sina.com at github
	I create the user password **.7

	like this I set the method

so I refer to the help of ssh from the github, and I get the message
	ssh -vT git@github.com | it works fine

ssh -vT git@repo.wisemapping.org:~coollimixsinacom/wisemapping/limix-wiseorg.git                                                   
*LIMIX_TOIMPROVE: ssh only support the host, not support the path*

	OpenSSH_5.3p1, OpenSSL 1.0.0-fips 29 Mar 2010
	debug1: Reading configuration data /etc/ssh/ssh_config
	debug1: Applying options for *
	ssh: Could not resolve hostname repo.wisemapping.org:~coollimixsinacom/wisemapping/limix-wiseorg.git: Name or service not known


ssh -vT git@repo.wisemapping.org | I get the ssh for the remote system.

	openSSH_5.3p1, OpenSSL 1.0.0-fips 29 Mar 2010
	debug1: Reading configuration data /etc/ssh/ssh_config
	debug1: Applying options for *
	debug1: Connecting to repo.wisemapping.org [192.241.203.149] port 22.
	debug1: Connection established.
	debug1: identity file /home/limix/.ssh/identity type -1
	debug1: identity file /home/limix/.ssh/id_rsa type -1
	debug1: identity file /home/limix/.ssh/id_dsa type 2
	debug1: Remote protocol version 2.0, remote software version OpenSSH_5.3
	debug1: match: OpenSSH_5.3 pat OpenSSH*
	debug1: Enabling compatibility mode for protocol 2.0
	debug1: Local version string SSH-2.0-OpenSSH_5.3
	debug1: SSH2_MSG_KEXINIT sent
	debug1: SSH2_MSG_KEXINIT received
	debug1: kex: server->client aes128-ctr hmac-md5 none
	debug1: kex: client->server aes128-ctr hmac-md5 none
	debug1: SSH2_MSG_KEX_DH_GEX_REQUEST(1024<1024<8192) sent
	debug1: expecting SSH2_MSG_KEX_DH_GEX_GROUP
	debug1: SSH2_MSG_KEX_DH_GEX_INIT sent
	debug1: expecting SSH2_MSG_KEX_DH_GEX_REPLY
	debug1: Host 'repo.wisemapping.org' is known and matches the RSA host key.
	debug1: *Found key in /home/limix/.ssh/known_hosts:13*
	debug1: ssh_rsa_verify: signature correct
	debug1: SSH2_MSG_NEWKEYS sent
	debug1: expecting SSH2_MSG_NEWKEYS
	debug1: SSH2_MSG_NEWKEYS received
	debug1: SSH2_MSG_SERVICE_REQUEST sent
	debug1: SSH2_MSG_SERVICE_ACCEPT received
	debug1: Authentications that can continue: *publickey*,*gssapi-keyex*,*gssapi-with-mic*,password
	debug1: Next authentication method: gssapi-with-mic
	debug1: Unspecified GSS failure.  Minor code may provide more information
	Credentials cache file '/tmp/krb5cc_500' not found

	debug1: Unspecified GSS failure.  Minor code may provide more information
	Credentials cache file '/tmp/krb5cc_500' not found

	debug1: Unspecified GSS failure.  Minor code may provide more information

	debug1: Next authentication method: publickey
	debug1: Offering public key: /home/limix/.ssh/id_dsa
	debug1: Remote: Forced command: gitorious coollimixsinacom
	debug1: Remote: Port forwarding disabled.
	debug1: Remote: X11 forwarding disabled.
	debug1: Remote: Agent forwarding disabled.
	debug1: Remote: Pty allocation disabled.
	debug1: Server accepts key: pkalg ssh-dss blen 434
	debug1: Remote: Forced command: gitorious coollimixsinacom
	debug1: Remote: Port forwarding disabled.
	debug1: Remote: X11 forwarding disabled.
	debug1: Remote: Agent forwarding disabled.
	debug1: Remote: Pty allocation disabled.
	debug1: Authentication succeeded (publickey).
	debug1: channel 0: new [client-session]
	debug1: Requesting no-more-sessions@openssh.com
	debug1: Entering interactive session.
	debug1: Sending environment.
	debug1: Sending env XMODIFIERS = @im=ibus
	debug1: Sending env LANG = en_US.utf8
	Welcome, coollimixsinacom. Use git to push/pull your repositories
	debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
	debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0

	debug1: channel 0: free: client-session, nchannels 1
	Transferred: sent 2416, received 3080 bytes, in 0.7 seconds
	Bytes per second: sent 3516.1, received 4482.5
	debug1: Exit status 1


>ssh git@repo.wisemapping.org

	PTY allocation request failed on channel 0
	*Welcome, coollimixsinacom. Use git to push/pull your repositories*
	Connection to repo.wisemapping.org closed.


# src.download #
There are three methods for the git. *git,http,ssh*

* git protocol 

	git clone git://repo.wisemapping.org/~coollimixsinacom/wisemapping/limix-wiseorg.git
	
	Initialized empty Git repository in /home/limix/media/workspace/limix-wiseorg/.git/
	repo.wisemapping.org[0: 192.241.203.149]: errno=Connection timed out
	fatal: unable to connect a socket (Connection timed out)
	
	*I think may be there is something wrong with me*
	git clone git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
	
	Initialized empty Git repository in /home/limix/media/workspace/linux/.git/
	remote: Counting objects: 2194366 
	
	*repo.wisemapping.org[0: 192.241.203.149]: errno=Connection timed out*
	>ping 192.241.203.149                                                                                                                       
	PING 192.241.203.149 (192.241.203.149) 56(84) bytes of data.
	64 bytes from 192.241.203.149: icmp_seq=1 ttl=51 time=275 ms
	64 bytes from 192.241.203.149: icmp_seq=2 ttl=51 time=288 ms
	64 bytes from 192.241.203.149: icmp_seq=3 ttl=51 time=279 ms
	64 bytes from 192.241.203.149: icmp_seq=4 ttl=51 time=298 ms
	64 bytes from 192.241.203.149: icmp_seq=5 ttl=51 time=348 ms
	--- 192.241.203.149 ping statistics ---
	6 packets transmitted, 5 received, 16% packet loss, time 5121ms
	rtt min/avg/max/mdev = 275.712/298.015/348.090/26.190 ms
	fatal: unable to connect a socket (Connection timed out)
	*LIMIX_TOIMPROVE: may by there is something wrong with the port for the git protocol*


* http protocol

	git clone https://git.repo.wisemapping.org/~coollimixsinacom/wisemapping/limix-wiseorg.git                                         

	Initialized empty Git repository in /home/limix/media/workspace/limix-wiseorg/.git/
	error: *Couldn't resolve host 'git.repo.wisemapping.org'* while accessing 
	https://git.repo.wisemapping.org/~coollimixsinacom/wisemapping/limix-wiseorg.git/info/refs

	refer to the http://tool.chinaz.com/dns/ | *这里有一个TTL设置为0,可以让某台主机只有自己会去解析*

	opendns 	A 	67.215.65.132 	美国 加利福尼亚州旧金山市OpenDNS有限责任公司 	0
	refer to the opendns i get the result

	>git clone https://67.215.65.132/~coollimixsinacom/wisemapping/limix-wiseorg.git           

	Initialized empty Git repository in /home/limix/media/workspace/limix-wiseorg/.git/
	error: Failed connect to 67.215.65.132:443; Operation now in progress while accessing 
	https://67.215.65.132/~coollimixsinacom/wisemapping/limix-wiseorg.git/info/refs
	fatal: HTTP request failed

	>ping 67.215.65.132

	PING 67.215.65.132 (67.215.65.132) 56(84) bytes of data.
	send http request, but no answer

	> traceroute git.repo.wisemapping.org

	traceroute to git.repo.wisemapping.org (67.215.65.132), 30 hops max, 60 byte packets
	 1  * * * 2  * * * 3  * * * 4  * * * 5  * * * 6  * * * 7  * * * 8  * * * 9  * * * 10  * * *
	11  * * * 12  * * * 13  * * * 14  * * * 15  * * * 16  * * * 17  * * * 18  * * * 19  * * * 20  * * *
	21  * * * 22  * * * 23  * * * 24  * * * 25  * * * 26  * * * 27  * * * 28  * * * 29  * * * 30  * * *


	> Refer wisemapping gov help
	*Adding this repository as a pushable origin:*

	Add the push url to your already existing origin:
	git remote set-url --push origin git@repo.wisemapping.org:~coollimixsinacom/wisemapping/limix-wiseorg.git
	# to push the master branch to the origin remote we added above:
	git push origin master
	# after that you can just do:
	git push

	*Cloning this repository:*

	git clone git://repo.wisemapping.org/~coollimixsinacom/wisemapping/limix-wiseorg.git limix-wiseorg
	cd limix-wiseorg

	*Add this repository as a remote to an existing local repository:*

	git remote add limix-wiseorg git://repo.wisemapping.org/~coollimixsinacom/wisemapping/limix-wiseorg.git
	git fetch limix-wiseorg
	git checkout -b my-local-tracking-branch limix-wiseorg/master_or_other_branch


	git remote set-url --push origin git@repo.wisemapping.org:~coollimixsinacom/wisemapping/limix-wiseorg

	*fatal: Not a git repository (or any of the parent directories): .git*
	出现这个问题后，发现其实是在本系统下没有找到一个.git这样的目录，所以在终端下使用git --help命令，显示了其主要的一些命令参数，发现一个参数是init：
	2.init Create an empty git repository or reinitialize an existing one
	执行git init之后，然后再重新编译，这个问题就被解决了。为什么和svn不一样，svn不需要自己使用命令来创建自己的资源库，
	而git需要自己使用命令手动创建，具体.git的位置和你在哪个目录下执行命令有关。


* ssh.protocol

	git clone limix-wiseorg git://repo.wisemapping.org/~coollimixsinacom/wisemapping/limix-wiseorg.git
	进入对应的目录,设置一下,Okey,Success.

