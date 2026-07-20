# cloudns-failoverlist

Auto-generated, auto-pushed list of ClouDNS DNS Failover node IPs
(`get-failover-servers.json`), used as firewall allowlist sources
(FortiGate External Resource, OPNsense URL Table alias) so ClouDNS's
health-check nodes can always reach monitored sites.

- `cloudns-all-v4.txt` / `cloudns-all-v6.txt` — one IP per line, plain text.
- Updated by a scheduled PowerShell script (`Update-CloudnsList.ps1`, not stored
  in this repo) running under the **SYSTEM** account.

## Testing / running manually

The update script must be run (or tested) **as SYSTEM**, not as a regular
admin user. Two things depend on that specific account context:

1. The SMTP credential file (`smtp-cred.xml`) is encrypted with `Export-Clixml`,
   which ties it to the account + machine that created it. It was generated
   as SYSTEM, so only SYSTEM can `Import-Clixml` it back.
2. The `Send-MailKitMessage` PowerShell module must be installed with
   `-Scope AllUsers` and be resolvable in a SYSTEM session.

To get an interactive SYSTEM shell for testing:

```powershell
PsExec.exe -i -s pwsh.exe
```

Then confirm with `whoami` (should show `nt authority\system`) before
running or testing the script.

## Notes

- List is intentionally public — it only ever contains ClouDNS's own
  published node IPs, nothing about our internal environment.
- Only specific scoped credentials (fine-grained PAT, Contents: Read/write,
  this repo only) have write access. Repo visibility is public-read only.
