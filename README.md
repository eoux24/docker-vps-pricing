# vps for docker: KVM plans from $21.99/year with same-price renewals, plus how to pick the right RAM tier

Running Docker on a VPS comes down to three requirements: KVM virtualization (not OpenVZ), full root access, and enough RAM for your containers plus their databases. RackNerd checks all three with KVM VPS plans starting at **$21.99/year** — and unlike most budget hosts, its promotional prices renew at the same rate instead of doubling.

If you want the short version: most people self-hosting a stack like Nextcloud, Gitea, n8n, or a reverse proxy behind containers should take the **2 GB annual plan at $35.99/year** (2 vCPU, 35 GB SSD, 5 TB traffic). Heavier setups with databases or Coolify want the 4 GB tier at $59.99/year.

> **Quick picks:** running a couple of containers with a database and a proxy → the **2 GB KVM plan, $35.99/year, 5 TB monthly traffic, 1 IPv4 included**, renewing at the same price. Just experimenting with Docker Engine on a sandbox → the 1 GB plan at $21.99/year works, though it gets tight once a database joins. 👉 [Get the 2 GB KVM VPS at $35.99/year](https://my.racknerd.com/aff.php?aff=11397&pid=953)

## Why "vps for docker" filters out half the cheap hosts

Docker depends on Linux kernel features — namespaces and cgroups — that only work properly when your virtual machine has its own kernel. That single fact explains most of the difference between hosts in this price range:

- **KVM** gives you a real VM with a dedicated kernel and your own RAM allocation. Docker Engine, Docker Compose, custom kernels, and custom ISOs all behave normally. Every RackNerd VPS plan uses KVM.
- **OpenVZ/LXC** containers share the host's kernel. Some budget providers still sell these as "VPS," and Docker installs on them either fail or hit arbitrary limits. It's the first thing worth checking at any price under $5/month, because the price tag won't tell you which technology is inside.

RAM is the second constraint. Docker Engine itself is light, but the typical stack — app container, PostgreSQL or MariaDB, Redis, a Traefik or Caddy proxy — eats into 2 GB quickly and genuinely struggles at 1 GB. RackNerd's own one-click app documentation sets the thresholds for its stack: n8n and Coolify are "comfortable from 2 GB," AnythingLLM, Ollama, and LibreChat want at least 4 GB, and OpenClaw wants 8 GB.

Bandwidth comes third, and it's where containerized apps surprise people. A 1 Gbps unmetered port moves a lot of data before you notice. RackNerd's annual plans include 3–20 TB per month depending on tier; the monthly plans trade bandwidth for storage.

## Every RackNerd plan for Docker, with prices

RackNerd sells KVM VPS on two tracks right now. The annual Specials line is the value play for Docker users; the standard monthly line offers more storage per dollar and no long commitment.

**Annual KVM Specials** (all include 1 free IPv4, 1 Gbps port, full root access, RAID-10 SSD, ctrl control panel, deploy in multiple locations):

| Plan | RAM / CPU | SSD | Traffic | Price | Order |
| --- | --- | --- | --- | --- | --- |
| 1 GB KVM | 1 GB / 1 vCPU | 20 GB | 3 TB/mo | $21.99/yr | [Order 1 GB](https://my.racknerd.com/aff.php?aff=11397&pid=952) |
| 2 GB KVM | 2 GB / 2 vCPU | 35 GB | 5 TB/mo | $35.99/yr | [Order 2 GB](https://my.racknerd.com/aff.php?aff=11397&pid=953) |
| 4 GB KVM | 4 GB / 3 vCPU | 60 GB | 7 TB/mo | $59.99/yr | [Order 4 GB](https://my.racknerd.com/aff.php?aff=11397&pid=954) |
| 6 GB KVM | 6 GB / 6 vCPU | 100 GB | 12 TB/mo | $89.99/yr | [Order 6 GB](https://my.racknerd.com/aff.php?aff=11397&pid=955) |
| 8 GB KVM | 8 GB / 7 vCPU | 150 GB | 20 TB/mo | $119.99/yr | [Order 8 GB](https://my.racknerd.com/aff.php?aff=11397&pid=956) |

**Standard monthly KVM plans** (Intel Xeon, RAID-10 SSD, 1 free IPv4, 1 Gbps):

| Plan | RAM / vCore | SSD | Traffic | Price | Order |
| --- | --- | --- | --- | --- | --- |
| 512 MB | 512 MB / 1 | 30 GB | 500 GB/mo | $26.99/yr | [Order 512 MB](https://my.racknerd.com/aff.php?aff=11397&pid=1) |
| 1 GB | 1 GB / 2 | 50 GB | 1 TB/mo | $17.99/mo | [Order 1 GB](https://my.racknerd.com/aff.php?aff=11397&pid=20) |
| 2 GB | 2 GB / 3 | 75 GB | 2 TB/mo | $20.59/mo | [Order 2 GB](https://my.racknerd.com/aff.php?aff=11397&pid=21) |
| 4 GB | 4 GB / 4 | 130 GB | 3 TB/mo | $24.59/mo | [Order 4 GB](https://my.racknerd.com/aff.php?aff=11397&pid=22) |
| 6 GB | 6 GB / 5 | 170 GB | 4 TB/mo | $27.59/mo | [Order 6 GB](https://my.racknerd.com/aff.php?aff=11397&pid=23) |
| 8 GB | 8 GB / 6 | 220 GB | 5 TB/mo | $36.59/mo | [Order 8 GB](https://my.racknerd.com/aff.php?aff=11397&pid=24) |
| 12 GB | 12 GB / 7 | 300 GB | 6 TB/mo | $55.99/mo | [Order 12 GB](https://my.racknerd.com/aff.php?aff=11397&pid=25) |

The two 2 GB options deserve a direct comparison, because this is the decision most Docker users actually face. The annual Special gives you **5 TB of traffic for roughly $3/month equivalent**, but only 35 GB of storage. The monthly plan gives you **75 GB of storage**, plus one more vCPU, but only 2 TB of traffic at $20.59/month — about seven times the annual cost. Containers that serve media or store photos (an Immich instance, a media server) burn through 35 GB fast; nearly everything else — VPNs, proxies, small web apps, CI sandboxes — cares more about bandwidth. Match the plan to which resource your containers actually consume.

## What Docker hosting actually costs over two years

Here's the comparison most "Docker VPS" listicles skip: the renewal price. Hostinger's KVM line is the most visible competitor in this search, and its sticker prices are promotional rates tied to long prepayments.

|  | RackNerd 2 GB Special | RackNerd 4 GB Special | Hostinger KVM 1 | Hostinger KVM 2 |
| --- | --- | --- | --- | --- |
| RAM / CPU | 2 GB / 2 vCPU | 4 GB / 3 vCPU | 4 GB / 1 vCPU | 8 GB / 2 vCPU |
| Storage | 35 GB SSD | 60 GB SSD | 50 GB NVMe | 100 GB NVMe |
| Traffic | 5 TB/mo | 7 TB/mo | 4 TB/mo | 8 TB/mo |
| Entry price | $35.99/yr | $59.99/yr | $6.49/mo (24 mo upfront) | $8.99/mo (24 mo upfront) |
| Renewal | same | same | $11.99/mo | $14.99/mo |
| First 2 years | **$71.98** | $119.98 | $155.76 | $215.76 |
| Year 3 | $35.99 | $59.99 | $143.88 | $179.88 |

Two honest observations from that table. First, RackNerd's 4 GB Special costs $59.99/year forever, which undercuts even Hostinger's *promotional* KVM 1 rate on an annual basis while offering the same RAM and more CPU. Second, Hostinger brings real advantages: NVMe storage, weekly backups, and a more guided dashboard for beginners. If you want hand-holding and pay-for-convenience, that's a legitimate trade-off — just budget for the renewal, which is where the gap widens to roughly $84–120 per year in RackNerd's favor.

One thing to know before ordering either way: RackNerd VPS is **unmanaged**. Support answers hardware, network, and panel questions around the clock, but OS updates, Docker upgrades, and backups are your job. If you want a provider to babysit your containers, neither of these is that product.

Location matters too. RackNerd runs 20+ datacenters across North America, Europe, and Asia — Los Angeles, New York, Dallas, Chicago, Seattle, San Jose, and more — and you pick the location at checkout. The Los Angeles site runs an Asia-optimized network (routed via Noction IRP), which is the right pick if most of your visitors connect from Asia. 👉 [Browse all RackNerd KVM plans and locations](https://bit.ly/RacKnerd)

## Getting Docker running on a RackNerd VPS

Setup takes minutes, not hours:

1. **Order and pick your OS.** Choose your datacenter location, then pick Ubuntu, Debian, CentOS, AlmaLinux, Rocky Linux, or Fedora. The VPS activates right after payment; the welcome email with your root password, IP, and panel login usually arrives within a few minutes.
2. **Install Docker two ways.** The easiest path is the ctrl control panel's one-click app: **Docker with Portainer** deploys in one click, and Portainer's web UI then handles most day-to-day container work. If you'd rather run plain Docker Engine, SSH in and install it yourself — full root access means nothing blocks you.
3. **Manage from ctrl.** Reboot, reinstall the OS, reset the root password, open an HTML5 VNC console for out-of-band recovery, and set inbound firewall rules. Switching distros later is a reinstall away; a custom ISO outside the standard list can be mounted via a support ticket.

Two details catch people off guard. IPv6 is available at the Los Angeles and France locations — up to 100 free addresses — but only if you open a support ticket after ordering; it's not automatic. And upgrades aren't zero-downtime: moving up a tier requires a reboot with about a minute of interruption. Starting at 2 GB and stepping up to 4 GB later is a perfectly sane strategy; just schedule the reboot when it's convenient.

## Which plan fits which Docker workload

Match the verified specs to what you're running:

- **One app + database + reverse proxy** (Gitea, Uptime Kuma, a small n8n instance): the 1 GB Special runs it, but memory will be tight with a database attached. The 2 GB plan is the safer default.
- **A self-hosted stack** (Nextcloud + Gitea + Traefik, or Coolify managing several apps): 2 GB at $35.99/year. RackNerd's own guidance puts Coolify comfortably at 2 GB. Third-party reviews of this exact plan describe "a handful of containers" as no problem, as long as you're deliberate about what runs simultaneously.
- **Database-heavy setups, larger n8n workflows, staging mirrors of production:** 4 GB at $59.99/year. This is the tier people wish they'd started on after outgrowing 2 GB.
- **Local AI tooling** (Ollama, LibreChat, AnythingLLM): start at 6 GB ($89.99/year) per the vendor's own RAM guidance; OpenClaw needs 8 GB ($119.99/year). Keep expectations calibrated: no plan includes a GPU, so these tiers suit CPU inference and app serving, not running large models locally.
- **Storage-hungry containers** (photo libraries, media servers): the monthly line's bigger SSD allocations fit better than the Specials, or plan around external object storage.
- **Where 2 GB visibly struggles:** large datasets in heavy databases, high-traffic e-commerce, anything spawning many concurrent processes. Those want 4 GB or more.

## FAQ

**Does the RackNerd Specials price go up at renewal?**
No. The official FAQ states the specials are "lifetime recurring" — you renew at the same rate for as long as you keep the service. That's the core difference from hosts whose first-year discount hides a much higher renewal rate.

**Is a RackNerd VPS good for a Docker beginner?**
Only if you're comfortable with basic SSH. The service is unmanaged, so installing and updating Docker is on you. The one-click Docker + Portainer install in ctrl removes the initial setup friction, and Portainer's web interface covers routine container management, but security patches and backups remain your responsibility.

**Annual Specials or monthly plans for Docker?**
For anything long-running, the annual Specials: more RAM and far more bandwidth per dollar. The monthly line makes sense when storage is the bottleneck (up to 75 GB at the 2 GB tier) or when you're testing something short-term and don't want a year-long commitment. One honest caveat on the low end: the 512 MB plan costs $26.99/year yet offers only 500 GB of monthly traffic, which makes it a poor fit for anything network-facing — the 1 GB Special at $21.99/year is cheaper and better in every respect.

## Before you click order

Decide the RAM tier first — 2 GB covers most container stacks, 4 GB if databases or Coolify are in the picture, 6–8 GB only for AI tooling. Then confirm two things at checkout: the datacenter location (Los Angeles for Asia-facing latency, otherwise pick whichever is nearest your users) and the OS (Ubuntu LTS or Debian keeps Docker installation friction low). There's no promo code to hunt for at this price point; the listed rates are the rates, and they renew as-is.

If that math works for you, 👉 [start with the 2 GB KVM VPS at $35.99/year](https://my.racknerd.com/aff.php?aff=11397&pid=953) and have your containers running before the welcome email cools down.
