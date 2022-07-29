---
id: 12957
title: '/etc/init.d/xl2tpd for CentOS'
date: '2011-11-03T02:06:54+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=12957'
permalink: /2011/11/03/12957
views:
    - '4787'
shorturl:
    - 'http://goo.gl/pfxY9'
duoshuo_thread_id:
    - '6.3356049082968E+18'
dsq_thread_id:
    - '4271399136'
posturl_add_url:
    - 'yes'
---

<pre class="lang:shell decode:1 " >
#!/bin/sh
#
# xl2tpd This shell script takes care of starting and stopping l2tpd.
#
# chkconfig: – 80 30
# description: Layer 2 Tunnelling Protocol Daemon (RFC 2661)
#
# processname: xl2tpd
# config: /etc/xl2tpd/xl2tpd.conf
# pidfile: /var/run/xl2tpd.pid
#Servicename
SERVICE=xl2tpd
# Source function library.
. /etc/rc.d/init.d/functions
# Source networking configuration.
. /etc/sysconfig/network
if [ ${NETWORKING} = "no" ]
then
	exit 0
fi
[ -x /usr/local/sbin/$SERVICE ] || exit 0
RETVAL=0

start() {
	echo -n "Restarting IPSec: "
	service ipsec restart

	echo -n "Starting $SERVICE: "
	if [ ! -d /var/run/xl2tpd ]
	then
		mkdir /var/run/xl2tpd
	fi
	daemon /usr/local/sbin/$SERVICE
	RETVAL=$?
	[ $RETVAL -eq 0 ] && touch /var/lock/subsys/$SERVICE
	echo ""
	return $RETVAL
}

stop() {
	echo -n "Stopping $SERVICE: "
	killproc $SERVICE
	RETVAL=$?
	echo
	[ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/$SERVICE
	return $RETVAL
}

restart() {
	stop
	start
}
# See how we were called.
case "$1" in
  start)
	start
	;;
  stop)
	stop
	;;
  status)
	status $SERVICE
	RETVAL=$?
	;;
  restart|reload)
	restart
	;;
  condrestart)
	[ -f /var/lock/subsys/$SERVICE ] && restart || :
	;;
  *)
	echo "Usage: $SERVICE {start|stop|status|restart|reload|condrestart}"
	exit 1
esac
</pre>