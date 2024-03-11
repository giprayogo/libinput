# README

Patched `libinput` for Thinkpad Z13 gen 1.
Applied [this](https://martin.baillie.id/wrote/avoiding-libinput-hysteresis-on-a-thinkpad/) patch by Martin Baillie.
See also [issue #286](https://gitlab.freedesktop.org/libinput/libinput/-/issues/286).

To-Do: add patch for custom acceleration profile (not exposed by KDE yet).
See e.g.:

- [`libinput_device_config_accel_set_profile()`](https://wayland.freedesktop.org/libinput/doc/latest/api/group__config.html#gac92eb3bcfb9a3e6f670c3ff18451be2f)
- [`libinput_config_accel_profile`](https://wayland.freedesktop.org/libinput/doc/latest/api/group__config.html#gad63796972347f318b180e322e35cee79)
- [`libinput_config_accel_set_points`](https://wayland.freedesktop.org/libinput/doc/latest/api/group__config.html#gaa7f3ed3b0722cdf9fb82d546a8507da4)
