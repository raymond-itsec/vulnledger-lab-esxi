# VulnLedger Lab - ESXi recipe

Optional reference recipe for running VulnLedger's 4-tier multihost
deployment on VMware ESXi free tier with Rocky Linux 10.1.

The application itself lives at
[github.com/raymond-itsec/vulnledger](https://github.com/raymond-itsec/vulnledger).

## What this recipe gives you

A repeatable path from a blank ESXi free-tier host to four booted
Rocky 10.1 VMs ready to run VulnLedger's multihost compose stack.
Build host can be macOS (Fusion Pro) or Linux / Windows (Workstation
Pro).

## What this recipe is NOT

A prerequisite. VulnLedger runs on bare metal, KVM, Proxmox, or any
provider's VPS that runs Docker on Linux. This recipe is one
operator-friendly path for the specific case of "I have an ESXi free
tier host and want to validate the multihost flow locally."

## Read in order

1. [Prerequisites](01-prerequisites.md)
2. [Build the OVA](02-build-the-ova.md)
3. [Deploy to ESXi](03-deploy-to-esxi.md)
4. [Verify](04-verify.md)
5. [Hand off to VulnLedger](05-handoff-to-vulnledger.md)
6. [Cleanup](06-cleanup.md)
