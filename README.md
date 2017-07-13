This small script can resolve AWS EC2 instance id and name tag to allow you to connect to your
box without resolving its ip address first. Useful if you start/stop your instance a lot but do not want Elastic IP for some reason.

Requires boto and aws credentials to work.
If you have awscli installed and configured you're all set, I guess.

Oh, and there must be debian-flavored netcat installed.

to automatically proxy all ssh connections to `*.ec2` hosts put this in your `~/.ssh/config`:
```
Host *.ec2
        ProxyCommand ~/bin/ec2-resolver-proxy "%h" "%p"
```

And now you can ssh into your EC2 instance with:
```
  ssh i-123456.ec2
  ssh myCoolNameTag.ec2
```
All tools that use ssh as backend (ansible, rsync) should work, too.

There are alternatives, of course:
http://travisjeffery.com/b/2015/11/ssh-into-ec2-instances-by-instance-id/
http://dev.bizo.com/2010/03/ssh-to-ec2-instance-id.html
