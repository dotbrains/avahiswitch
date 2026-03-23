# avahiswitch

[![License: PolyForm Shield 1.0.0](https://img.shields.io/badge/License-PolyForm%20Shield%201.0.0-blue.svg)](https://polyformproject.org/licenses/shield/1.0.0/)

Raspberry Pi service to turn on `avahi-daemon` if `/boot/avahi` is present.

## Use

In order to use the [`avahiswitch.service`](avahiswitch.service) you must add a file called `avahi` in the `/boot/` directory (`touch /boot/avahi`). This will enable the `avahi-daemon`, which in turn makes the Raspberry Pi discoverable via the name `raspberry-pi.local`, which can be changed by editing `etc/hostname`.

Additionally, you must edit both `/boot/cmdline.txt` and `/boot/config.txt` to enable `ethernet gadget mode`.

*   `/boot/cmdline.txt`: Add `modules-load=dwc2,g_ether` after `rootwait`
*   `/boot/config.txt`: Add `dtoverlay=dwc2`

This is particularly useful when using `ethernet gadget mode` for the initial headless setup of a Raspberry Pi.

I advise to disable the `avahi-daemon` service after the initial setup (`systemctl disable avahi-daemon`).

## Install

To install the service, use the following snippet: 


```
wget -O /lib/systemd/system/avahiswitch.service https://github.com/nicholasadamou/avahiswitch/raw/master/avahiswitch.service && \
    wget -O /etc/avahi/avahi-daemon.conf https://github.com/nicholasadamou/avahiswitch/raw/master/avahi-daemon.conf && \ 
    sudo systemctl enable avahiswitch.service && sudo systemctl enable avahiswitch.service
```

## License

This project is licensed under the [PolyForm Shield License 1.0.0](https://polyformproject.org/licenses/shield/1.0.0/) — see [LICENSE](LICENSE) for details.