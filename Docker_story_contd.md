
# 🧪 Chapter 12: The First Container Comes Alive

The industry had containers.
Docker had won developer hearts ❤️

But one question still mattered:

> **What actually happens when we type `docker run`?**

This chapter is where the magic becomes **mechanical**.

---

## ▶️ The Moment of Truth: `docker run`

When you run:

```bash
docker run nginx
````

It looks simple.

But under the hood, Docker performs a **carefully orchestrated chain of events**.

📌 This is where *containerisation stops being theory*.

---

## 🧠 Step-by-Step: What Happens Internally

### Step 1️⃣: Docker CLI Talks to Docker Daemon

🗣️

* `docker` (CLI) sends a request to `dockerd`
* This happens via REST API (Unix socket / TCP)

📖 Reference:
[https://docs.docker.com/engine/api/](https://docs.docker.com/engine/api/)

---

### Step 2️⃣: Image Resolution & Pull

📦
Docker checks:

* Is the image available locally?
* If not → pulls from registry

Layers are downloaded **only if missing**.

📌 This is why images are fast after first pull.

📷 Image layers reference:
[https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/](https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/)

---

### Step 3️⃣: containerd Takes Control

⚙️
Docker daemon hands over responsibility to **containerd**.

containerd:

* Manages container lifecycle
* Prepares filesystem snapshots
* Talks to low-level runtime

📌 Docker ≠ runtime
Docker = **manager**

📖 containerd overview:
[https://containerd.io/](https://containerd.io/)

---

### Step 4️⃣: runc Creates the Container

🧬
This is the **birth moment** of a container.

`runc`:

* Creates Linux namespaces
* Applies cgroups
* Sets root filesystem
* Starts the process

📌 **At this moment — the container is just a Linux process.**

📷 Runtime stack diagram:
[https://www.docker.com/blog/what-is-containerd-runtime/](https://www.docker.com/blog/what-is-containerd-runtime/)

---

### Step 5️⃣: The Linux Kernel Does the Real Work

🐧
Kernel enforces:

* Isolation (namespaces)
* Limits (cgroups)
* Scheduling (CPU)
* Memory allocation

Docker steps back.
The kernel takes over.

📌 Containers live and die by the kernel.

---

## 🔍 Chapter 13: Containers Are Not Special (Truth Bomb 💣)

Here’s the most important realisation:

> **A container is just a process with restrictions.**

No VM.
No hypervisor.
No fake OS.

Just:

* `ps`
* `top`
* `kill`

With a restricted view of reality.

📖 Proof reading:
[https://jvns.ca/blog/2016/10/10/what-even-is-a-container/](https://jvns.ca/blog/2016/10/10/what-even-is-a-container/)

---

## 🧠 Chapter 14: Namespaces — Creating Alternate Realities

To the process inside the container:

* It thinks it is PID 1
* It thinks it owns the network
* It thinks it has its own filesystem

But all of this is an **illusion created by namespaces** 🪄

### Types of Illusions

| Illusion                     | Namespace |
| ---------------------------- | --------- |
| “I’m PID 1”                  | PID       |
| “This is my network”         | NET       |
| “This is my root filesystem” | MNT       |
| “This is my hostname”        | UTS       |

📌 Each container lives in its own *bubble of reality*.

📖 Deep reference:
[https://man7.org/linux/man-pages/man7/namespaces.7.html](https://man7.org/linux/man-pages/man7/namespaces.7.html)

---

## 📊 Chapter 15: cgroups — Teaching Containers Discipline

Namespaces isolate.
But isolation alone is dangerous.

What if one container eats all memory? 🧨

That’s where **cgroups** step in.

cgroups:

* Limit CPU
* Limit memory
* Throttle I/O
* Prevent noisy neighbours

```bash
docker run --memory=512m --cpus=1 nginx
```

📌 Exceed limits → Kernel intervenes (OOMKill)

📖 Kernel guide:
[https://www.kernel.org/doc/html/latest/admin-guide/cgroup-v2.html](https://www.kernel.org/doc/html/latest/admin-guide/cgroup-v2.html)

---

## 🧱 Chapter 16: Filesystems — The Illusion of a Private Disk

Containers *appear* to have their own filesystem.

In reality:

* Images are read-only
* Containers get a writable layer
* OverlayFS merges everything

```text
Image layers (read-only)
↑
Container writable layer
```

📌 Delete the container → data is gone
📌 Volumes exist because of this reality

📖 Storage driver docs:
[https://docs.docker.com/storage/storagedriver/](https://docs.docker.com/storage/storagedriver/)

---

## 🌐 Chapter 17: Networking — Containers Learn to Talk

Processes alone are useless.
They must communicate.

Docker creates:

* Virtual Ethernet pairs (veth)
* Linux bridges
* NAT rules
* Embedded DNS

Containers talk using:

* Service names
* Container names
* Not IPs ❌

📌 Networking is abstracted — but real.

📖 Networking deep dive:
[https://docs.docker.com/network/](https://docs.docker.com/network/)

---

## 🔄 Chapter 18: The Container Lifecycle (Life & Death)

A container’s life is short and intentional.

```
Created → Running → Stopped → Removed
```

Containers are **cattle, not pets** 🐄
Kill them. Recreate them. Trust automation.

📌 This mindset enables scaling and healing.

---

## 🧭 Where the Story Goes Next

At this point in the journey:

* You know **why containers exist**
* You know **how they are born**
* You know **what they really are**

The next chapters naturally become:

👉 **How do multiple containers work together?**
👉 **How do we describe systems, not commands?**
👉 **How do we scale without losing sanity?**

That’s where **Docker Compose and orchestration** enter the story.

---

## ▶️ Next Chapter Options (Your Choice)

Reply with one 👇
1️⃣ **Docker Images & Dockerfiles — crafting containers**
2️⃣ **Docker Networking — packet-level intuition**
3️⃣ **Docker Volumes — data survival story**
4️⃣ **Docker Compose — from one container to systems**

We’ll continue the story 📖🔥
