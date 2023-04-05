# Cjacker's sway login manager

A framebuffer stupidly simple graphical login manager and greeter for greetd.

- sway only, with session selection support, only start sway by `startway` wrapper script.
- framebuffer only, without dependency on X or another wayland session such as cage to start the login manager.
 
# Prior work:

SwayLM is forked from [Deathowl's DDLM](https://github.com/deathowl/ddlm).

DDLM is forked from [Kenylevinsen's DLM](https://git.sr.ht/~kennylevinsen/dlm).

# Setup
- Install greetd.
- git clone the sources and built it with `cargo build --release`.
- install `target/release/swaylm` to `/usr/bin`.
- install `assets/startsway` to `/usr/bin`.
- create a config file `config.toml` at `/etc/greetd/` as:
```
[terminal]
# The VT to run the greeter on. Can be "next", "current" or a number
# designating the VT.
vt = 1

# The default session, also known as the greeter.
[default_session]
command = "swaylm"

# The user to run the command as. The privileges this user must have depends
# on the greeter. A graphical greeter may for example require the user to be
# in the `video` group.
user = "greetd"
```
NOTE, some distributions may use `greeter` user instead of `greetd`, make sure the user in `video` group.

I also put a copy at [assets/config.toml](./assets/config.toml).

- switch to greetd by:
```
sudo systemctl disable <previous dm>
sudo systemctl enable greetd
sudo systemctl restart greetd
```

# Why need startsway wrapper script

You need handle a lot of env vars and settings before starting sway, also need setup dbus daemon properly, etc.

A wrapper script is useful to handle all these works.

# Why only sway

I use i3wm for decades and never switch to and use other desktop environment. 

In practice, trying different DE is a kind of waste of time.

# Future plans:
- Accept default username as argument and only requires inputing password to login.
