# README

Patched `libinput` for my Thinkpad Z13 gen 1 Touchpad.
Two patches:

- No "wobbling detection" (presumably related to hysteresis?). [This](https://martin.baillie.id/wrote/avoiding-libinput-hysteresis-on-a-thinkpad/) patch by Martin Baillie.
  See also [issue #286](https://gitlab.freedesktop.org/libinput/libinput/-/issues/286).
- Linear acceleration by [american_spacey on Reddit](https://www.reddit.com/r/kde/comments/o5lk7q/comment/h2not3j/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

To-Do: Experiment with other acceleration profiles such as one in [this paper](http://direction.bordeaux.inria.fr/~roussel/publications/2011-UIST-libpointing.pdf)

(probably relevant APIs)

- [`libinput_device_config_accel_set_profile()`](https://wayland.freedesktop.org/libinput/doc/latest/api/group__config.html#gac92eb3bcfb9a3e6f670c3ff18451be2f)
- [`libinput_config_accel_profile`](https://wayland.freedesktop.org/libinput/doc/latest/api/group__config.html#gad63796972347f318b180e322e35cee79)
- [`libinput_config_accel_set_points`](https://wayland.freedesktop.org/libinput/doc/latest/api/group__config.html#gaa7f3ed3b0722cdf9fb82d546a8507da4)
