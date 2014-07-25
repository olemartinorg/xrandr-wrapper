xrandr-wrapper
==============

### Why?
My nVidia card doesn't support more than two outputs at once (including the laptop monitor). I usually use two external monitors. In order to switch from my laptop monitor to the externals I have to:

* First turn on one of the external outputs (DP-0), while the laptop output (LVDS-0) is on
* Turn off the laptop output (LVDS-0)
* Turn on the second external output (DP-1)

In some instances, i already have the VGA-0 output turned on, and I'll want to turn that off first before i start this procedure. With even more variables, storing a procedure as the one above in a script (like `switch-to-office-monitors.sh`) soon becomes a minefield of uncertainties - and if you do one step wrong, you might end up disabling all your outputs and kill your X server.

### How?
This script is my attempt to remedy this problem, making stuff like the above recipe easy to put in a script. Xrandr-wrapper will query xrandr first to see which outputs are enabled at the time, then turn off all but one of them, and then turn on the rest (perhaps using the step-by-step method as described above). Hopefully one of the already-on outputs are also in the list of outputs you want enabled - if not, xrandr-wrapper will do the dance for you even then.

### Usage
You can use this script just like you would use xrandr, except that instead of specifying what you want *changed*, you specify the *end result*. So, let's say that you'd normally tell xrandr to `--output DP-1 --auto --primary --rotate left`. Xrandr would try to enable the DP-1 output in *addition* to what you already have set up. Xrandr-wrapper, on the other hand, will try to end up with DP-1 being the *only* output enabled.

### Why not disper?
Good question. Last time I used disper, it seemed to skip xrandr completely and communicate directly with the nvidia driver. Sadly, it wasn't as good at for example rotating outputs as xrandr is. When the proprietary nvidia driver started supporting xrandr. I threw disper out the door, and I've never looked back.
