# route53_grim_reaper

This repo is going to find stale route53 entries and destroy them from orbit
1) grab all known route entries (default to `rhdemo.io` for me).  This is configurable by variable `workshop_dns_zone`
2) check with [ec2_instance_info module](https://docs.ansible.com/ansible/latest/modules/ec2_instance_info_module.html) to make sure there is no IP address for the associated tag.  This logic could be a ping... but still thinking about how that would look.
3) reap

![grim reaper](death.jpg)

# How to use

Make sure you have AWS setup to work with route53 modules, then run this ansible-playbook

```ansible-playbook reap.yml```

The Ansible Playbook will pause and prompt you (not suitable for Ansible Tower) before it tries to delete entries.


## Example Snippet

The Ansible Playbook will display a list of the record entries, then prompt you to continue and then nuke them from orbit, destroying their precious planet and resources.  Thus you can take back route53 and earn mad credits.

```
TASK [these are marked for deletion - verficiation list] ***************************************************************************************************************************
ok: [localhost] => {
    "msg": [
        "please delete record entries [u'student5.005c.rhdemo.io', u'student6.005c.rhdemo.io', u'student7.005c.rhdemo.io', u'student8.005c.rhdemo.io', u'student9.005c.rhdemo.io', u'student10.0097.rhdemo.io', u'student11.0097.rhdemo.io']"
    ]
}

TASK [pause] ***********************************************************************************************************************************************************************
[pause]
If you press enter, it will now delete these entries:
ok: [localhost]

TASK [delete dns entries marked for deletion] **************************************************************************************************************************************
changed: [localhost] => (item=student5.005c.rhdemo.io)
changed: [localhost] => (item=student6.005c.rhdemo.io)
changed: [localhost] => (item=student7.005c.rhdemo.io)
changed: [localhost] => (item=student8.005c.rhdemo.io)
changed: [localhost] => (item=student9.005c.rhdemo.io)
changed: [localhost] => (item=student10.0097.rhdemo.io)
changed: [localhost] => (item=student11.0097.rhdemo.io)
```

# Author

[@IPvSean](twitter.com/ipvsean) likes reaping
