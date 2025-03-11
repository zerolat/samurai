# Samurai

The ultimate Linux kernel optimized for low-latency workloads like Edge computing, VoIP, Gaming, and VPN. Featuring eBPF, XDP, and stripped-down overheads for maximum performance.

## Build Steps
1. Install dependencies:
   ```bash
   sudo apt update && sudo apt install -y build-essential libncurses-dev bison flex libssl-dev libelf-dev bc dwarves pahole git
   ```
2. Clone the repo:
   ```bash
   git clone https://github.com/0xAFz/samurai.git
   cd samurai
   ```
3. Download kernel source (e.g., 6.1.x):
   ```bash
   wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.1.x.tar.xz
   tar -xvf linux-6.1.x.tar.xz
   cd linux-6.1.x
   ```
4. Copy the config:
   ```bash
   cp ../.config .

   make olddefconfig
   ```
5. Build the kernel:
   ```bash
   make -j$(nproc)
   ```
6. Install (optional):
   ```bash
   sudo make modules_install
   sudo make install
   ```

## Debian Package Build Steps
1. Install packaging tools:
   ```bash
   sudo apt install -y fakeroot kernel-package
   ```
2. Build the `.deb` package:
   ```bash
   make -j$(nproc) deb-pkg
   ```
3. Find the output files (e.g., `linux-image-*_amd64.deb`) in the parent directory.

## Contributions
Got ideas to make it faster? Fork the repo, tweak it, and send a PR. We welcome optimizations!
