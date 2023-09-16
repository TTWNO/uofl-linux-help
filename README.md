# yeehaw (Some Linux Help for UofL students)

## Using GitLab

Most Linux users prefer to use their terminal instead of web interfaces (when possible).
There is a tool for Github called [`gh`](https://cli.github.com) that brings Github to the command line.
There is a similar tool (although not quite as widely available in package repositories) called [`glab`](https://docs.gitlab.com/ee/editor_extensions/gitlab_cli/), which allows you to work with the official [GitLab instance](https://gitlab.com), or a self-hosted version (like the one offered by UofL).
I highly recommend using the tool to interact with the [UofL Gitlab (only available on VPN)](http://gitlab.cs.uleth.ca/).
Remember that it only supports HTTP authentication, and that you will need to create a new person access token to login to `glab` with.
The personal access token link can be given to you through the `glab auth login` command.

```bash
$ glab auth login
```

In addition, I highly recommend adding an SSH key both from your personal laptop, and your UofL Linux box account (given to you by your instructor).
Follow the standard procedure to create an SSH key, then add your public key (`.pub`) to your Gitlab account using:

```bash
$ glab ssh-key add <key_file> -t name-of-key
```

## Connecting to `eduroam`

If using NetworkManager (especially `nmcli`), you can load a file using the following command:

```bash
$ nmcli con load <file>
```

I have provided an `eduroam.nmconnection` file that you can load into NetworkManager with the command above, then activate it with:

```bash
$ nmcli con up eduroam
```

Make sure to replace the placeholders before loading and connecting.

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

