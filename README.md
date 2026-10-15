# `BARK`

`BloodHound Attack Research Kit` — a PowerShell toolkit for researching and continuously validating Azure / Entra abuse primitives. Fork of [BloodHoundAD/BARK](https://github.com/BloodHoundAD/BARK), synced to current upstream.

## `What it does`

* Validates every documented Azure abuse primitive against a live tenant — MS Graph, AzureRM, Entra ID, Intune, Key Vault.
* `Invoke-AllAzureRMAbuseTests` and `Invoke-AllAzureADAbuseTests` run the full primitive battery for a given privilege set and report what actually worked.
* ~105 functions, zero third-party dependencies. Each function is standalone — rip any one out and use it in your own scripts.
* Results feed straight into BloodHound attack-path validation: prove the edge exists, or stop assuming it does.

## `Quick start`

```powershell
Import-Module .\BARK.ps1

# graph-scoped abuse tests (needs an MS Graph app role)
Invoke-ExternalAbuseTest -Token $MGToken

# full AzureRM battery
Invoke-AllAzureRMAbuseTests `
    -GlobalAdminClientID "<sp-client-id>" `
    -GlobalAdminSecret "<secret>" `
    -TenantName "target.onmicrosoft.com" `
    -SubscriptionID "<sub-id>"
```

Threaded functions need `PowerShell 7+`.

## `Notes`

* This is a **fork**. All credit for BARK goes to `Andy Robbins (@_wald0)` and the BloodHound team — this copy just keeps an updated mirror under Foxcorn Lab with their original authorship and GPLv3 license intact.
* Abuse tests touch live Azure objects and leave audit trails. Run them in a lab tenant you own, not someone else's production.

## `Thanks to`

* `Andy Robbins (@_wald0)` and the BloodHound / SpecterOps crew for building and open-sourcing BARK.

> Research by `Vineeth Kumar` (`foxcornlab`). Found a bug or want a feature, open an `issue`.
