---
layout: post
title: "Understanding the exchange between SFTP Client and SFTP Server"
description: "An article on what goes on between an SFTP Client and SFTP Server"
comments: true
keywords: "file transfer protocols, security, sftp, server, client"
---

This was an article written for a secure file transfer product.

[Read more here](https://www.sftpplus.com/articles/2018/sftpplus-exchange-sftp-server-client.html)

---

# Full content below

## Why read this?

As part of meeting the Accounting component of the AAA (Authorization, Authentication and Accounting) framework, each event and action on the server and/or the client-side are recorded by SFTPPlus. 
These events have an associated Event ID which is also publicly searchable both on our website and on the internal documentation included in the software package that you have downloaded.

System and network administrators touching on logs - be it in the most verbose format or not - may find this article describing the breakdown of such logs helpful.

For this example, we will be touching on SFTPPlus SFTP transfers from both the client-side and server-side only.
Please do not hesitate to get in touch with us if you are interested in learning more about other file transfer protocols.


## SFTPPlus SFTP Server-side Perspective

### Initial configuration notes

If you are currently evaluating SFTPPlus, please follow our documentation to learn more about how you can configure your database and event handlers to suit your specifications.

`Read more about configuring databases </documentation/sftpplus/latest/configuration/databases.html>`_ with SFTPPlus.

`Read more about configuring event handlers </documentation/sftpplus/latest/configuration/event-handlers.html>`_.
These provide further ways to configure SFTPPlus to create logging actions based on the events recorded.

Even if you are an existing customer, you can follow our documentation links above in order to refresh your knowledge on configuring SFTPPlus version 3.
For those on legacy versions, please consult the documentation relevant to your version.


### Example logs from SFTPPlus

The following are snippets when logging in for the first time from a GUI client to an SFTPPlus 3.30.0 SFTP server.

A new connection has been made to the service `sftp-1`.
Knowing the service name is useful in case there are multiple other SFTP services running::

    | 30014 2018-02-27 17:28:53 sftp-1 Unknown 127.0.0.1:58032
      New SSH connection made.
    | 2018-02-27 17:28:53 30014 New SSH connection made.

The following are authentication methods associated with the server and confirmation of which methods are not active.
There may be more methods, depending on how many of these are set up and enabled.
To simplify the login process, please make sure to disable all unused authentication methods.::

    | 20138 2018-02-27 17:28:55 some-http-auth-uuid Unknown 127.0.0.1:58032
      Ignoring http authentication "auth-over-remote-http" for "user" since it
      is not active.
    | 2018-02-27 17:28:55 20138 Ignoring http authentication "auth-over-remote-http"
      for "user" since it is not active.
    | 20138 2018-02-27 17:28:55 ldap-uuid Unknown 127.0.0.1:58032 Ignoring
      ldap authentication "LDAP against local test server" for "user" since it
      is not active.

The following logs list out a successful authentication of `user` using the `ssh-key`::

    | 20137 2018-02-27 17:28:55 test-server-uuid Unknown 127.0.0.1:58032
      Account "user" of type "application" authenticated as "user" by
      application authentication "Application Accounts" using ssh-key.
    | 2018-02-27 17:28:55 20137 Account "user" of type "application"
      authenticated as "user" by application authentication "Application
      Accounts" using ssh-key.

The following log message confirms the type of permissions allowed for the account and an active transfer that is already running::

    | 20182 2018-02-27 17:28:55 Process user 127.0.0.1:58032 Account "user"
      logged in with permissions [[u'allow-full-control'], [u'/main_folder/*', u'allow-full-control'],
      [u'*.PDF', u'allow-read']]. Files uploaded as: test.txt

The following confirms that the user has logged into and now has access to the folder as the root ("/") folder::

    | 30011 2018-02-27 17:28:55 Process user 127.0.0.1:58032 Subsystem SFTP
      successfully started in "/root/home/node/user/" as "/".
    | 2018-02-27 17:28:55 30011 Subsystem SFTP successfully started in
      "/root/home/node/user/" as "/".
    | 30060 2018-02-27 17:28:55 Process user 127.0.0.1:58032 Canonical file
      name requested for ".".
    | 2018-02-27 17:28:55 30060 Canonical file name requested for ".".
    | 30060 2018-02-27 17:28:55 Process user 127.0.0.1:58032 Canonical file
      name requested for "/.".
    | 2018-02-27 17:28:55 30060 Canonical file name requested for "/.".
    | 30019 2018-02-27 17:28:55 Process user 127.0.0.1:58032 Listing folder "/".
    | 2018-02-27 17:28:55 30019 Listing folder "/".
    | 30020 2018-02-27 17:28:55 Process user 127.0.0.1:58032 Successfully
      listed folder "/".
    | 2018-02-27 17:28:55 30020 Successfully listed folder "/".


## SFTPPlus SFTP Client-side Perspective


### Initial configuration notes

If you are currently evaluating SFTPPlus, please follow our `client side documentation </documentation/sftpplus/latest/operation-client/>`_.

The SFTPPlus Client software utilizes the command-line client-shell to access remote file servers using the `interactive shell </documentation/sftpplus/latest/operation-client/client-shell>`_.

Even if you are an existing customer, you can follow our documentation links above in order to refresh your knowledge on configuring SFTPPlus version 3.
For those on legacy versions, please consult the documentation relevant to your version.


### Example logs from SFTPPlus

Let's connect with SFTPPlus Client using the SFTP protocol on port 10022.
The following log details the UUID of the `sftp` service and confirms the connections::

    | $ ./bin/client-shell.sh sftp://user@localhost:10022 -p pass
      --ssh-server-fingerprint 06:cb:46:2b:9a:9a:c4:10:54:f0:ea:2f:b6:05:cb:a0
    | SFTPPlus (3.31.0) file transfer client shell
    | > connect
    | 20140 2018-03-05 16:40:59 51e1db00-8214-4b68-96fe-58470b8b2fc5 Process
      0.0.0.0:0 Connecting resource "sftp".
    | 30072 2018-03-05 16:40:59 Process user localhost:10022 Location sftp
      connected to the SSH server.
    | 30076 2018-03-05 16:40:59 Process user localhost:10022 Client SFTP
      subsystem initialized for location sftp.
    | 20141 2018-03-05 16:40:59 51e1db00-8214-4b68-96fe-58470b8b2fc5 Process
      0.0.0.0:0 Resource "sftp" successfully connected.
    | 20156 2018-03-05 16:40:59 51e1db00-8214-4b68-96fe-58470b8b2fc5 Process
      0.0.0.0:0 Successfully started location "sftp" of type sftp.

On the event that the SFTP connections fails, the log will state a number of details.
The event ID is `30073`. The event will communicat the host key algorithm that is in use to identify the server-side, the cipher used to receive data, the HMAC for both sent and received data, key exchange algorithm, cipher used for sent data and the name of the location associated for this event.
Below is an example of the event that has been emitted has part of this new SFTP connection.::

    | 30073 2018-03-05 16:36:16 Process user localhost:10022 Connection to
      SSH server was lost for location sftp. Protected using host-key:ssh-rsa key-exchange:
      diffie-hellman-group-exchange-sha256 in-hmac:hmac-sha2-256
      in-cipher:aes256-ctr out-hmac:hmac-sha2-256 out-cipher:aes256-ctr

Providing that the SFTP connection succeeds, supported actions are logged as either a success like below::

    | > gattrs remote_get
    | 60071 2018-03-05 16:41:22 Process Process 0.0.0.0:0 Successfully got
      attributes for "Reports_2018" on "sftp".
    | name: Reports_2018
    | path: Reports_2018
    | size: 128
    | modified: 2018-02-16 16:15:21
    | is_file: False
    | is_folder: True
    
Or error details are caught with an explanation message as to why::

    | > get unknown_file
    | 20145 2018-03-05 16:42:08 Process Process 0.0.0.0:0 Failed to resolve
      text for event id "60054" with data "{'path': 'unknown_file\xc8\x9bu',
      'location': u'sftp', 'avatar':
      <chevah.server.identity.avatar.ProcessAvatar object at 0x10efc3110>,
      'details': "'ascii' codec can't decode byte 0xc8 in position 9: ordinal
      not in range(128)"}". 'ascii' codec can't decode byte 0xc8 in position
      9: ordinal not in range(128)


## SFTPPlus SFTP Exchange - Detailed Verbose OpenSSH Logs


### Initial configuration notes

Following from that, you can use the built-in the client-side or server-side software that you are utilizing.
SFTPPlus offers logging functionalities both for the client-side and server-side.
Network administrators using other software, such as `sftp -vvv`, for client or server may wish to use additional logging functionalities.


### Example with sftp -vvv output

These lines mean that SSH protocol 2.0 is being utilized with the version of OpenSSH::

    debug1: Enabling compatibility mode for protocol 2.0
    debug1: Local version string SSH-2.0-OpenSSH_7.6

This line indicates which protocol version is in use service-side and which version::

    debug1: Remote protocol version 2.0, remote software version SFTPPlus_3.30.0

This indicates which algorithms are preferred.
You may opt to only select the strongest availability supported in your system first.
In this case the ordering is logical as it moves from the more secure algorithm down to a less secure algorithm.::

    | debug3: order_hostkeyalgs: prefer hostkeyalgs:
      ssh-rsa-cert-v01@openssh.com,rsa-sha2-512,rsa-sha2-256,ssh-rsa

These are the key exchange algorithms that are available.::

    | debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,
      ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,
      diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,
      diffie-hellman-group18-sha512,diffie-hellman-group-exchange-sha1,
      diffie-hellman-group14-sha256,diffie-hellman-group14-sha1,ext-info-c

These are the host key algorithms.::

    | debug2: host key algorithms: ssh-rsa-cert-v01@openssh.com,rsa-sha2-512,
      rsa-sha2-256,ssh-rsa,ecdsa-sha2-nistp256-cert-v01@openssh.com,
      ecdsa-sha2-nistp384-cert-v01@openssh.com,
      ecdsa-sha2-nistp521-cert-v01@openssh.com,ssh-ed25519-cert-v01@openssh.com,
      ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-ed25519

These are the ciphers used from client to server (`ctos`) and from server to client (`stoc`)::

    | debug2: ciphers ctos: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,
      aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com

    | debug2: ciphers stoc: chacha20-poly1305@openssh.com,aes128-ctr,
      aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com

These are the ciphers used from client to server (`ctos`) and from server to client (`stoc`)::

    | debug2: MACs ctos: umac-64-etm@openssh.com,umac-128-etm@openssh.com,
      hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,
      hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,
      hmac-sha2-256,hmac-sha2-512,hmac-sha1

    | debug2: MACs stoc: umac-64-etm@openssh.com,umac-128-etm@openssh.com,
      hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,
      hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,
      hmac-sha2-256,hmac-sha2-512,hmac-sha1

These are the compression algorithms used from client to server (`ctos`) and from server to client (`stoc`)::

    debug2: compression ctos: none,zlib@openssh.com,zlib
    debug2: compression stoc: none,zlib@openssh.com,zlib

This is the key exchange initialized proposal from the host server::

    | debug2: peer server KEXINIT proposal
    | debug2: KEX algorithms: diffie-hellman-group-exchange-sha256,
      diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1,
      diffie-hellman-group14-sha1
    | debug2: host key algorithms: ssh-dss,ssh-rsa
    | debug2: ciphers ctos: 
      aes256-ctr,aes256-cbc,aes192-ctr,aes192-cbc,aes128-ctr,aes128-cbc,
      3des-ctr,3des-cbc
    | debug2: ciphers stoc:
      aes256-ctr,aes256-cbc,aes192-ctr,aes192-cbc,aes128-ctr,aes128-cbc,
      3des-ctr,3des-cbc
    | debug2: MACs ctos: hmac-sha2-256,hmac-sha1
    | debug2: MACs stoc: hmac-sha2-256,hmac-sha1
    | debug2: compression ctos: none,zlib
    | debug2: compression stoc: none,zlib

These are the key exchange algorithms used from server to client and client to server::

    | debug1: kex: algorithm: diffie-hellman-group-exchange-sha256
    | debug1: kex: host key algorithm: ssh-rsa
    | debug1: kex: server->client cipher: aes128-ctr MAC: hmac-sha2-256
      compression: none
    | debug1: kex: client->server cipher: aes128-ctr MAC: hmac-sha2-256
      compression: none

This is the SSH version 2 key exchange Diffie-Hellman Group Exchange request.
This specifies the size of the SSH prime moduli being calculated by the SFTP server as indicated in the SFTPPlus `/configuration/` file.
When you first initialize SFTPPlus version 3, the Time Type Tests Tries Size Generator Modulus is generated and saved in `ssh-service.moduli`.
This file contains primes ranging in size from 1023 to 8191 bits.
An example of the contents for the .moduli file is below::

    | 20060827134212 2 6 100 3071 2 
      D3230D237572ECE9F92358715EBAC3A4D89F2D6B4DC39F056450263BEF1665FBD
      7B93916ABC867B7064802159D273C7EB01C5F9281A3D6DCCB7CF997D385998EC0E1FA3319AFE771A90ADBACEB414A02
      0630D7C7F161FAFEC6C9FC06D3205C712AAE8848A1B2C21DFF301C7FFC0B75D13F060A313C32AFEEAF1493F641760EB
      EF38829B3371699D2A3264D0ECEB4E5C19581ED8C57699F559B9828BBFE147952E289F0E171C9C60335DD2F492CB409
      A4DB97BDF86E2DBA605064DB040A3DF5678E24F66718CA115C95C892FF7AEDFAABC2E6414716298CEC1A604270FEADF
      191B7C8A59C238C395A65442C0B963BF83025BED3951A271B7440EC7687C31DE63355DA7FEAC15DC962C7BF7614EB59
      B077B9889AD8703DFE98AC99615B722A0ABE89956D1058E025C7733420CB51D7E1608EFF2C0A30C9A5EB77CCA02C6B0
      0CE781B172001C6C458630890062E27CE307D513A7686A69D1D548DE8334B13136D9E842A5E17FD67522C93823E03F0
      8AEE8024AF5D88B2EE01D4D9980084EFD5D943

In the following example below, a SSH moduli prime from 2048 to 8192 bits are used.
Specifically, a moduli with a range from 4092 to 8192 are sent for the SSH message key exchange Diffie-Hellman group exchange request as indicated on `debug1` line below (`SSH2_MSG_KEX_DH_GEX_REQUEST(2048<8192<8192)`)
Once sent, the server uses the moduli file, the same file that was initialized as part of the SFTPPlus installation steps, in order to crack the shared secret.
The server provides its host key back to the client along with the algorithm used as indicated by the final line as `Server host key: ssh-rsa SHA256:hdSfa7gb2O984malHerkwerj3m20dHb6Yuwl0&hbxFj`.

See the rest of the output below::

    | debug1: SSH2_MSG_KEX_DH_GEX_REQUEST(2048<8192<8192) sent
    | debug3: receive packet: type 31
    | debug1: got SSH2_MSG_KEX_DH_GEX_GROUP
    | debug2: bits set: 4092/8192
    | debug3: send packet: type 32
    | debug1: SSH2_MSG_KEX_DH_GEX_INIT sent
    | debug3: receive packet: type 33
    | debug1: got SSH2_MSG_KEX_DH_GEX_REPLY
    | debug1: Server host key: ssh-rsa
      SHA256:hfSfa0gb2O884malLerkwerj3m20dBb6Yuwl0&hbxGj

The client then checks to see if the host key is located within the `known_hosts` file::

    | debug3: hostkeys_foreach: reading file "/root/home/node/.ssh/known_hosts"
    | debug3: record_hostkey: found key type RSA in file
      /root/home/node/.ssh/known_hosts:8
    | debug3: load_hostkeys: loaded 1 keys from [12.345.678.90]:10022

A few more steps occur to verify this server host name and port::

    ddebug1: Host '12.345.678.90]:10022' is known and matches the RSA host key.
    ddebug1: Found key in /root/home/node/.ssh/known_hosts:8

This is the server rekey interval::

    debug1: rekey after 4294967296 blocks
    debug1: SSH2_MSG_NEWKEYS sent
    debug1: expecting SSH2_MSG_NEWKEYS
    debug3: receive packet: type 21
    debug1: SSH2_MSG_NEWKEYS received
    debug2: set_newkeys: mode 0
    debug1: rekey after 4294967296 blocks

The following are SSH keys found::

    debug2: key: imported-openssh-key (0x7e403ff95550), agent
    debug2: key: /root/home/node/.ssh/id_rsa (0x0)
    debug2: key: /root/home/node/.ssh/id_dsa (0x0)
    debug2: key: /root/home/node/.ssh/id_ecdsa (0x0)
    debug2: key: /root/home/node/.ssh/id_ed25519 (0x0)

The following are authentication methods that can continue, the preferred authentication order, remaining preferred::

    | debug3: send packet: type 5
    | debug3: receive packet: type 6
    | debug2: service_accept: ssh-userauth
    | debug1: SSH2_MSG_SERVICE_ACCEPT received
    | debug3: send packet: type 50
    | debug3: receive packet: type 51
    | debug1: Authentications that can continue: password,publickey
    | debug3: start over, passed a different list password,publickey
    | debug3: preferred publickey,keyboard-interactive,password
    | debug3: authmethod_lookup publickey
    | debug3: remaining preferred: keyboard-interactive,password
    | debug3: authmethod_is_enabled publickey
    | debug1: Next authentication method: publickey
    | debug1: Offering public key: RSA
      SHA256:F8zPRFytcYU8PERggkPDs+D32TRgvVm4H3BBJduo+de
      /root/home/node/.ssh/id_rsa
    | debug3: send_pubkey_test
    | debug3: send packet: type 50
    | debug2: we sent a publickey packet, wait for reply

The server will go through the exchange to authenticate until the final preferred method is reached - the password method.
Upon success, the client enters an interactive session with the server.

There will also be additional verbose logs after entering an interactive session, such as a brief snippet below::

  debug2: fd 6 setting TCP_NODELAY
  debug3: ssh_packet_set_tos: set IP_TOS 0x08
  debug2: client_session2_setup: id 0
  debug1: Sending environment.
  debug3: Ignored env _system_type
  debug1: Sending env LANG = en_CA.UTF-8
  debug2: channel 0: request env confirm 0
  debug3: send packet: type 98
  debug3: Ignored env _system_arch
  debug3: Ignored env XPC_FLAGS
  debug3: Ignored env _system_version
  debug3: Ignored env XPC_SERVICE_NAME
  debug3: Ignored env rvm_version
  debug3: Ignored env _system_name
  debug1: Sending subsystem: sftp

