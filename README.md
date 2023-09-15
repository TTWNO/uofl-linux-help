# yeehaw (Some Linux Help for UofL students)

## Connecting to `eduroam`

If using NetworkManager (especially `nmcli`), you can load a file using the following command:

```bash
$ nmcli con load <file>
```

I have provided an `eduroam.nmconnection` file that you can load into NetworkManager with the command above, then activate it with:

```bash
$ nmcli con up eduroam
```

## Connecting to the VPN

Since most Linux users are open-source extermist, it may be worth noting that UofL uses a proprietary *Cisco* product to connect to its VPN.
There is an open-source tool which implements the AnyConnect protocol, called `openconnect` (you can find it in your package repos with `pacman -Ss` or `apt search`).

Due to the way Microsoft implements their authentication, you need to go through quite the process every time you connect to the VPN using `openconnect`.

First, run the following command:

```bash
$ openconnect --protocol=anyconnect vpn.uleth.ca -g ULethbridgeVPN -u <uofl_linux_username> --cookie-on-stdin
```

Now, open a browser, and navigate to `vpn.uleth.ca`.
This should show you a blank page once you are signed in.
If it does not, then open a second tab and navigate to the same URL.

Once you get the blank page, get the `webvpn` cookie value (via developer tools).
Finally, paste that into the terminal where you ran your `anyconnect` command.
You should successfully connect to the VPN.

## Contributions

Send a PR or make an issue to help make these instructions better.

