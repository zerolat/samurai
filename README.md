# Samurai

Samurai is a **high-performance, low-latency** Linux kernel optimized for workloads that demand extreme responsiveness. It is **not a generic-use kernel**—it is stripped down to the bare essentials, built for **Edge, VoIP, Gaming, and VPNs**, where every microsecond counts.

## ⚠️ Warnings & Limitations

- **Not designed for general-purpose use.** Samurai is highly optimized and minimal—don’t expect it to work on your smart fridge. 🧊
- **Security mitigations removed.** To maximize performance, Samurai disables mitigations like Spectre/Meltdown patches. Use in trusted environments.
- **Minimal driver support.** Unused modules, drivers, and file systems have been stripped out. Check compatibility before use.
- **Logging & debugging overhead eliminated.** Samurai prioritizes raw performance over diagnostics. If you need extensive logs, this isn't the kernel for you.

## 🔥 Key Features

- **Extreme Low Latency:** Configured with **PREEMPT** and fine-tuned scheduling for ultra-responsive performance.
- **Tickless Kernel (NO_HZ_FULL @ 1000Hz):** Eliminates unnecessary timer interrupts, reducing overhead in real-time workloads.
- **Lightweight & Minimal:** Unused modules, drivers, and file systems removed for a streamlined footprint.
- **Security & Debugging Overheads Removed:** No **SELinux, CPU mitigations, or excessive logging**, ensuring maximum efficiency.
- **Optimized I/O Performance:** Uses **mq-deadline** scheduler for reduced disk latency.
- **eBPF/XDP Ready:** JIT always enabled for high-performance packet processing in networking applications.

## 🚀 Build & Install

### 1️⃣ Install Dependencies
```bash
sudo apt update && sudo apt install -y build-essential libncurses-dev bison flex libssl-dev libelf-dev bc dwarves pahole git
```

### 2️⃣ Clone Samurai Repository
```bash
git clone https://github.com/0xAFz/samurai.git
cd samurai
```

### 3️⃣ Download Kernel Source (e.g., 6.1.x)
```bash
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.1.x.tar.xz
tar -xvf linux-6.1.x.tar.xz
cd linux-6.1.x
```

### 4️⃣ Apply Samurai Config
```bash
cp ../.config .
```

### 5️⃣ Build the Kernel
```bash
make -j$(nproc)
```

### 6️⃣ Install (Optional)
```bash
sudo make modules_install
sudo make install
```

## 📦 Debian Package Build (Optional)

### 1️⃣ Install Packaging Tools
```bash
sudo apt install -y fakeroot
```

### 2️⃣ Build `.deb` Package
```bash
fakeroot make -j$(nproc) deb-pkg
```

### 3️⃣ Find the Output Files
Generated **.deb** files (e.g., `linux-image-*_amd64.deb`) will be in the parent directory.

## 🤝 Contributions
Samurai is built for speed, but there's always room for improvement. Have ideas? **Fork the repo, tweak it, and submit a PR.** We welcome optimizations and performance hacks!
