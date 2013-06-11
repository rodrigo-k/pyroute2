pyroute2
========

Python netlink library. The main goal of the project is to
implement complete NETLINK\_ROUTE family as well as several
other families (NETLINK\_NETFILTER etc.)

Current feature status see in STATUS.md

sample
------

More samples you can read in the project documentation.
Low-level interface::

    from pyroute2 import IPRoute

    # get access to the netlink socket
    ip = IPRoute()

    # print interfaces
    print ip.get_links()

    # stop working with netlink and release all sockets
    ip.release()

High-level transactional interface, IPDB:

    from pyroute2 import IPDB
    # local network settings
    ip = IPDB()
    # create bridge and add ports and addresses
    # transaction will be started with `with` statement
    # and will be committed at the end of the block
    with ip.create(kind='bridge', ifname='rhev') as i:
        i.add_port(ip.em1)
        i.add_port(ip.em2)
        i.add_ip('10.0.0.2/24')


The project contains several modules for different types of
netlink messages, not only RTNL.

installation
------------

`make install` or `pip install pyroute2`

requires
--------

Python >= 2.6

  * test reqs (optional): **python-coverage**, **python-nose**
  * plugin reqs (optional):
    * ptrace: **python-ptrace**

changelog
---------

* 0.1.9
    * tests: all races fixed
    * ipdb: half-sync commit(): wait for IPs and ports lists update
    * netlink: use pipes for in-process communication
    * Python 2.6 compatibility issue: remove copy.deepcopy() usage
    * QPython 2.7 for Android: works
* 0.1.8
    * complete refactoring of class names
    * Python 2.6 compatibility issues
    * tests: code coverage, multiple code fixes
    * plugins: ptrace message source
    * packaging: RH package
* 0.1.7
    * ipdb: interface creation: dummy, bond, bridge, vlan
    * ipdb: if\_slaves interface obsoleted
    * ipdb: 'direct' mode
    * iproute: code refactored
    * examples: create() examples committed
* 0.1.6
    * netlink: tc ingress, sfq, tbf, htb, u32 partial support
    * ipdb: completely re-implemented transactional model (see docs)
    * generic: internal fields declaration API changed for nlmsg
    * tests: first unit tests committed
* 0.1.5
    * netlink: dedicated io buffering thread
    * netlink: messages reassembling
    * netlink: multi-uplink remote
    * netlink: masquerade remote requests
    * ipdb: represent interfaces hierarchy
    * iproute: decode VLAN info
* 0.1.4
    * netlink: remote netlink access
    * netlink: SSL/TLS server/client auth support
    * netlink: tcp and unix transports
    * docs: started sphinx docs
* 0.1.3
    * ipdb: context manager interface
    * ipdb: [fix] correctly handle ip addr changes in transaction
    * ipdb: [fix] make up()/down() methods transactional [#1]
    * iproute: mirror packets to 0 queue
    * iproute: [fix] handle primary ip address removal response
* 0.1.2
    * initial ipdb version
    * iproute fixes
* 0.1.1
    * initial release, iproute module

links
-----

* home: https://github.com/svinota/pyroute2
* bugs: https://github.com/svinota/pyroute2/issues
* pypi: https://pypi.python.org/pypi/pyroute2
* docs: http://peet.spb.ru/pyroute2/
* list: https://groups.google.com/d/forum/pyroute2-dev
