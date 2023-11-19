# linux tips and tricks
:warning: **Please don't use this as a replacement for documentation.** :warning:

A repo where I try to document simple tricks I've found over the years.

Note: Suggestions are always welcome! Feel free to create a pull request if you feel like something is incorrect or needs revision.


# TODO:
- [ ] nvidia
  - [ ] Hardware acceleration
  - [ ] Loading nvidia kernel modules


# Table of contents
- [nvidia](#nvidia)

# NVIDIA
Since I own an nvidia gpu, I figured I'd create a section specific to nvidia.

## 1) Fix tearing and other performance improvements
:warning: **In order to change these settings, you'll likely need root perms.** :warning:
### nvidia-settings
Install the latest `nvidia` driver using `yay` or another [AUR](https://aur.archlinux.org/) helper. This should also install the `nvidia-settings` package, which is very important to improve the performance of our system. 

Run `nvidia-settings` and select "X Server Display Configuration" and select "advanced". Press `Force Composition Pipeline` and check if thescreen tearing remains. If it doesn't work, `Force Full Composition Pipeline` should do the trick. Make sure vsync is enabled by going over to OpenGL settings and select `Sync to VBlanc` if your system supports it. After performing these steps, press Save to X Configuration File and confirm. 

Next, go over to nvidia-settings Configuration and disable all active timers and press Save Current Configuration. This will improve performance. 

For a more in-detail guide, refer to [nvidia-settings](https://wiki.archlinux.org/title/NVIDIA#nvidia-settings). There's a few more settings that might be useful, such as `Coolbits` or `TripleBuffer` that I recommend reading about.

Lastly, make sure you run `nvidia-settings --load-config-only` every time you start your system. This could be done in several ways, but I recommend using either your window manager or desktop environment. See [Autostart](https://wiki.archlinux.org/title/Autostarting) for more.

### Compositor
A compositor is a great tool to make your desktop even better! However, despite not requiring much configuring to work (if any at all), compositors can sometimes cause performance issues. 

For the purpose of this tutorial, we'll be using `picom`. Aside from animations or other tiny details, working with a custom fork (such as `picom-ibhagwan-git`) will likely not yield any different results.

Install `picom` or `picom-git` and make sure to run `cp /etc/xdg/picom.conf` (or `/etc/xdg/picom.conf.example`) `.config/picom/picom.conf`. 

Open `picom.conf` and make sure to enable `vsync` by uncommenting `vsync = True` and check if it improved performance in any way. Lastly, make sure to play around with `backend`: `glx` and `egl` are more modern and might work better than the old `xrender`, but make sure to test each one individually and select the one that works best for you.
