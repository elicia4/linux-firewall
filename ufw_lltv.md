# UFW
[***go back to README***](README.md)

---

Notes on this video by LearnLinuxTV: https://youtu.be/XtRXm4FFK7Q

Keep in mind not to enable the iptables service as long as you use ufw for 
managing it. 

Update everything before installing ufw:

    apt upgrade && apt dist-upgrade

Install ufw:

    apt install ufw

You can check the status with:

    systemctl status ufw

Having the firewall installed isn't enough, it needs to be configured. Set the 
default rules for ufw. For that, run:

    ufw default allow outgoing

If your server is trying to reach something from the internet, you will want it
to reach whatever it's trying to reach. Then set the default for incoming:

    ufw default deny incoming

Don't rush this, you will get locked out of your system if this is not 
configured properly. You need to allow SSH in order to manage your firewall:

    ufw allow SSH

UFW knows that ssh is port 22, that's why you can do that. If you have ssh on a 
different port, make sure to configure this differently. To check the status:

    ufw status 

It will say inactive, that's why you haven't been dropped yet. To enable, run:

    ufw enable

Figure out your public IP address to do the next step. You can lock down SSH to
your public IP:

    ufw allow from <ip> to any port 22 proto tcp

To delete an entry, look at the list of entries first with:

    ufw status numbered

The entries will be numbered. To delete a particular rule, type:

    ufw delete <number>

As a general rule of thumb, only allow what's necessary.
