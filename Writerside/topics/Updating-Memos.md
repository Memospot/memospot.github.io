# Updating Memos

In general, you should download and install new versions of Memospot when they
are [released](https://github.com/memospot/memospot/releases). They come
bundled with the latest tested Memos server version.

> An auto-updater is planned, but it's not yet available.

## Memos server standalone update

While a standalone server update works in most cases, manual updates are
strongly discouraged for anything other than a **Patch** version release.

> The semantic version scheme used by Memos is `Major.Minor.Patch`. {style=note}

> Standalone updates can break things due to database and API changes
> that occur between Major and Minor versions. The current version of Memospot
> may not yet be prepared to handle them.
>
> If that's the case, you won't be able to revert the server binary to a
> previous working version without also reverting to a database backup matching the server
> version. {style=warning}

### Script-aided procedure {collapsible="true" default-state="collapsed"}

For convenience, there are server updater-scripts with auto-backup
capabilities.

#### Windows

Open PowerShell and run the following command:

```Shell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/memospot/memospot/main/memos-server-updater.ps1'))
```

> You can check the script source
> [here.](https://github.com/memospot/memospot/blob/main/memos-server-updater.ps1)
>

> You must run PowerShell as Admin if you are using Memospot `MSI` installers,
> as they do a system-wide installation.
>
> This is **not** necessary when using the NSIS/exe installer,
> as it only installs the application for the current user.
> {style=warning}
>

#### Linux/macOS

Open a terminal and run the following command:

```Shell
curl -fsSL https://raw.githubusercontent.com/memospot/memospot/main/memos-server-updater.sh | sudo bash
```

> You can check the script source
> [here.](https://github.com/memospot/memospot/blob/main/memos-server-updater.sh)
>

> You must run the script with sudo, as the Memospot `deb` package installs Memos to `/usr/bin/`.
> {style=warning}

The script can take an optional argument to specify a tag to update to. E.g. `… bash -s v0.21.0`.

### Manual procedure {collapsible="true" default-state="collapsed"}

> Do not proceed without taking a backup of your database.
>
> Close Memospot and copy the `memos` server binary and the `memod_prod`
> database file(s) to a location outside your working scope for extra safety.
> {style="warning"}

The basic update process is to download the latest Memos' server release from
[memos-builds](https://github.com/memospot/memos-builds/releases) and
replace the `memos` binary in the Memospot installation folder.

#### From Memos v0.18.2 to v0.21.0 {collapsible="true" default-state="collapsed"}

**This only applies to this version range, where the web front end wasn't
embedded.**

The downloaded build contains a `dist` folder (the web front end). You must
place it in the appropriate folder:

- Linux: `/usr/lib/memospot/`
- macOS: `$HOME/Library/Application Support/com.memospot.app/`
- Windows `%LocalAppData%\memospot`
