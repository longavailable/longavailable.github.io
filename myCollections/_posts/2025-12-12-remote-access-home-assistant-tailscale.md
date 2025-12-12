---
layout: post
title:  Access home assistant remotely using Tailscal Funnel
author: Bruce Liu
#last update date
date:   2025-12-12 20:50:00 +0800
#first published date
published: 2025-12-12 20:50:00 +0800
categories: [post]
tags: [home assistant, tailscale, cloudflare, intranet penetration]
description: 
header-image: 
permalink: /remote-ha-access-tailscale/
---
[Home Assistant] alives the devices at our home. That's really cool! Here are a way to access [Home Assistant] remotely by using tailscale.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# [tailscale]

## Installing [tailscale add-on]

Settings → Add-ons → Add-on store → Search `tailscale` → install

## Logging into a [tailscale] virtual network

Open web UI → connect (login/authenticate with your [tailscale] account)

Right now, you will have a `homeassistant` machine in your tailnet [console]. Add you can access your [homeassistant] using the [tailscale] ip and/or domain with a `8123` port through an HTTP connection (default) in the devices whose connected with your tailnet. While if you want to visit your [homeassistant] through an HTTPS connection and from devices without installed [tailscale] vpn client, you have to dive more deep.

## Enabling HTTPS

Add the following lines in your `configuration.yaml`:

```yaml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 127.0.0.1
```

Reload `configuration.yaml`: Developer tools → Restart → Quick reload

Settings → Add-ons → Tailscale → Configuration → Show unused optional configureation options → Share Home Assistant with Serve or Funnel → choose `serve` → save → Restart the add-on

Navigate to your tailnet [DNS page] of the admin [console]:

- Enable MagicDNS under MagicDNS section if not already enabled

- Enable HTTPS under HTTPS Certificates section

Now, you can access [homeassistant] using the **full domain** through an HTTPS and WITHOUT a port number in the devices connected to tailnet.

While, if you want to access using the tailnet ip, you have to using the HTTP connection with the `8123` port.

## Configing Tailscale Funnel

Add a Funnel node attribute following the [guide](https://tailscale.com/kb/1223/funnel#funnel-node-attribute).

- Open the [Node attributes] on the [Access controls] page of the admin [console].

- Add node attribute, then choose targets and attributes.

And go back to `Share Home Assistant with Serve or Funnel` on configuration page of tailscale add-on. Choose `funnel`, save, and restart the add-on.

Now, you can access [homeassistant] using the **full domain** through an HTTPS and WITHOUT a port number in any devices whether it did or didn't connect your tailnet.

## Custom domain

If you have a custom domain, you can redirect to the **full domain** with ther tailscale funnel service.

## References

[Remotely access Home Assistant via Tailscale for free](https://tailscale.com/blog/remotely-access-home-assistant)

<!--links-->
[cpolar]: https://tailscale.com/
[tailscale add-on]: https://github.com/hassio-addons/addon-tailscale
[homeassistant]: https://www.home-assistant.io/
[console]: https://login.tailscale.com/admin/machines
[DNS page]: https://login.tailscale.com/admin/dns
[Node attributes]: https://login.tailscale.com/admin/acls/visual/node-attributes
[Access controls]: https://login.tailscale.com/admin/acls/visual/general-access-rules
