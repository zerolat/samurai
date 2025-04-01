# Samurai

Samurai is a **high-performance, low-latency** Linux kernel optimized for workloads that demand extreme responsiveness. It is **not a generic-use kernel**—it is stripped down to the bare essentials, built for **Edge, VoIP, Gaming, and VPNs**, where every microsecond counts.

## ⚠️ Important Considerations

- **Specialized Kernel:** Not for general use. Optimized for specific workloads; compatibility with all hardware/software not guaranteed.
- **Reduced Security:** Performance prioritized over comprehensive security mitigations. Use in trusted environments only.
- **Minimal Drivers:** Limited hardware support due to the removal of unused drivers. Verify compatibility.
- **No Extensive Debugging:** Focus on performance means minimal logging and debugging features. Troubleshooting may be more challenging.

## 🔥 Key Features

- **Ultra-Low Latency:** **PREEMPT** enabled with a high-frequency tick rate (**1000Hz**) for exceptional responsiveness in critical applications.
- **Responsive Scheduling:** Fine-tuned policies ensure timely execution and a smooth, reactive system.
- **Lightweight Footprint:** Stripped of unnecessary components for reduced overhead and faster boot.
- **Performance-Focused:** Excludes **SELinux, significant CPU mitigations, and heavy logging** to maximize efficiency.
- **Accelerated I/O:** **mq-deadline** scheduler for minimized disk latency and improved application speed.
- **High-Speed Networking:** **eBPF/XDP JIT** enabled for advanced, high-performance packet processing.

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

---

## Boot Time Performance

The results below showcase a significant improvement compared to the default Debian kernel.

**Testing Environment for Samurai Kernel:**

* **VM:** KVM Infra (**Shared resources**)
* **CPU:** 2 Cores
* **RAM:** 4GB

**Samurai Kernel Boot Time:**

* **Kernel Boot Time:** 0.6 seconds
* **Full System Boot Time (to userspace):** 2 seconds

**Comparison with Default Debian Kernel:**

The default Debian kernel was previously tested on a server with the following specifications:
* **VM:** KVM Infra (**Shared resources**)
* **CPU:** 4 Cores
* **RAM:** 8GB

**Default Debian Kernel Boot Time (Approximate):**

* **Kernel Boot Time:** 3 seconds
* **Full System Boot Time (to userspace):** 6 seconds

**Performance Improvement:**

Based on these tests, the **Samurai** kernel demonstrates a remarkable improvement in boot time, even when running on a virtual machine with fewer resources:

* **Kernel Boot Time Improvement:**
    * Improvement: 3 seconds - 0.6 seconds = 2.4 seconds
    * Percentage Improvement: (2.4 / 3) * 100 = **80% faster** than the default Debian kernel boot time.

* **Full System Boot Time Improvement:**
    * Improvement: 6 seconds - 2 seconds = 4 seconds
    * Percentage Improvement: (4 / 6) * 100 ≈ **66.67% faster** than the default Debian full system boot time.

These results highlight the effectiveness of the optimizations implemented in the **Samurai** kernel, delivering significantly faster boot times and a quicker time to a usable system, even on resource-constrained and **shared cloud environments**.

---

## 🤝 Contributions
Samurai is built for speed, but there's always room for improvement. Have ideas? **Fork the repo, tweak it, and submit a PR.** We welcome optimizations and performance hacks!
