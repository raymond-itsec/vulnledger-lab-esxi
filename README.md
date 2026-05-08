# VulnLedger Lab (ESXi)

Reference operator recipe for running [VulnLedger](https://github.com/raymond-itsec/vulnledger)'s 4-tier multihost deployment on VMware ESXi free tier with Rocky Linux 10.1.

📖 **Read the recipe**: [raymond-itsec.github.io/vulnledger-lab-esxi](https://raymond-itsec.github.io/vulnledger-lab-esxi/)

> **This repo is one operator path, not a prerequisite.**
> VulnLedger runs on bare metal, KVM, Proxmox, ESXi, OVH/Hetzner/Scaleway/Contabo VPSes, or anything else that runs Docker on Linux. If your shop already has provisioning tooling (Terraform, Ansible, your provider's API, your favorite cloud-init flow), use that. This recipe exists for operators who want a worked example of a free, self-hosted lab built from scratch.

## What this repo will provide (work in progress)

Content is being extracted from private build notes. Until each item lands, refer to the application repo's [deployment docs](https://raymond-itsec.github.io/vulnledger/deployment/) for the connectivity contract that any provisioning path must satisfy.

| Planned content | Purpose |
|---|---|
| `packer/rocky-10.1.pkr.hcl` | Packer template (Fusion Pro on macOS or Workstation Pro on Linux / Windows) producing a Rocky Linux 10.1 OVA |
| `packer/kickstart/` | Unattended-install config |
| `packer/provisioners/` | Base hardening, Docker CE, wireguard-tools, nftables |
| `cloud-init/vl-{edge,app,data,monitoring}.yaml.template` | Per-role cloud-init injected via OVF properties at deploy time |
| `scripts/esxi-deploy.sh` | ovftool wrapper to deploy the OVA 4 times with role-specific properties |
| `nftables/samedc-{edge,app,data,monitoring}.nft` | Reference firewall rulesets when all 4 hosts share a private network |
| `nftables/crossdc-{edge,app,data,monitoring}.nft` | Reference firewall rulesets when hosts are geographically distributed and only WireGuard ties them together |

## What this repo deliberately does NOT contain

- The VulnLedger application itself (backend, frontend, compose files, etc.) - all that lives in the [main repo](https://github.com/raymond-itsec/vulnledger).
- Production deployment scripts. The path here targets a free-tier homelab; production deployments should pin specific versions, use a real CI/CD flow, and adapt to the operator's environment.

## Why ESXi free + VMware desktop hypervisor + ovftool

ESXi free disables the vSphere API write surface that Packer's `vsphere-iso` builder needs (paid vCenter required). Workaround: build the OVA locally with `vmware-iso` driving Fusion Pro on macOS or Workstation Pro on Linux / Windows, then deploy to ESXi with `ovftool` (bundled with both, supported on free ESXi). Both Fusion Pro and Workstation Pro are zero-cost for non-commercial use as of late 2024; ESXi free has been zero-cost for non-commercial use since the same period.

If you'd rather use Proxmox, KVM/libvirt, or a paid cloud, the same shape works - swap the builder and deploy step for whatever your platform expects. The compose tier files in the application repo don't change.

## Status

The docs site scaffolding (mkdocs + GitHub Pages workflow + terminal theme) is live; recipe content is being filled in incrementally as upstream issues close. Track progress on the [issues page](https://github.com/raymond-itsec/vulnledger-lab-esxi/issues).

## License

Same terms as the application repo. See [LICENSE](LICENSE).
