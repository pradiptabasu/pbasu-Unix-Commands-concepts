# pbasu-Unix-Commands-concepts

# SSH Tunnels, Port forwards and Authentication only priviledge
* https://www.youtube.com/watch?v=JKrO5WABdoY
* https://serverfault.com/questions/56566/ssh-tunneling-only-access
* https://unix.stackexchange.com/questions/14312/how-to-restrict-an-ssh-user-to-only-allow-ssh-tunneling

ssh tunneling only access
Yes, just use /bin/false as shell and instruct the user to start the tunneling SSH process without executing any remote command (i.e. the -N flag for OpenSSH):

ssh -N -L 1234:target-host:5678 ssh-host

On the server side, you can restrict this by setting their user shell to /bin/true. This will allow them to authenticate, but not actually run anything since they don't get a shell to run it in. This means they will be limited to whatever subset of things SSH is able to offer them. If it offers port forwarding, they will still be able to do that.

On the client side, you will probably want to connect with the -N. This stops the client from ASKING for a remote command such as a shell, it just stops after the authentication part is done.

