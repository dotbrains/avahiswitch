# avahiswitch

Raspberry Pi service to turn on `avahi-daemon` if `/boot/avahi` is present.

## Use

In order to use the [`avahiswitch.service`](avahiswitch.service) you must add a file called `avahi` in the `/boot/` directory (`touch /boot/avahi`). This will enable the `avahi-daemon`, which in turn makes the Raspberry Pi discoverable via the name `kali-pi.local`.

Additionally, you must edit both `/boot/cmdline.txt` and `/boot/config.txt` to enable `enthernet gadget mode`.

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

The code is available under the [MIT license](LICENSE).