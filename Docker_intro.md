# Docker & Containerisation – A Story Before the Technology

Before Docker became a command we typed daily, it was a **problem looking for survival** in the real world of operations.

This is the story of **why containers exist**.

---

## Chapter 1: The Age of Bare Metal (Before 2000)

In the early days, applications ran directly on **physical servers**.

### How things worked
- One server = one application
- OS installed manually
- Libraries installed by hand
- Configuration lived in human memory

### The problem
- Servers were expensive
- Hardware was underutilised
- Deployments were slow
- One broken app could bring down everything

Operations was fragile.
Scaling meant **buying new hardware**.

---

## Chapter 2: Virtual Machines – The First Revolution (2000–2010)

Then came **virtualisation**.

A single physical machine could now run:
- Multiple **virtual machines**
- Each with its own OS
- Strong isolation

This changed everything.

### What VMs solved
- Better hardware utilisation
- Isolation between applications
- Faster provisioning (hours → minutes)

### What VMs broke
- Heavy resource usage (full OS per VM)
- Slow boot times
- Large disk footprints
- Complex management

Teams started asking:
> “Why do we need a full OS just to run one app?”

---

## Chapter 3: Google’s Internal Secret (The Invisible Containers)

While the industry struggled with VMs, **Google** quietly solved the problem internally.

They realised:
- Applications don’t need a full OS
- They only need:
  - CPU
  - Memory
  - Filesystem
  - Network isolation

Google began running **millions of isolated processes** on shared kernels using:
- Linux namespaces
- cgroups

This internal system later inspired:
- Borg
- Omega
- Kubernetes

But at this time, **no one outside Google could use it**.

---

## Chapter 4: Linux Grows Superpowers (2006–2012)

The Linux kernel quietly evolved.

Key features matured:
- **Namespaces** → isolation
- **cgroups** → resource control
- **chroot** → filesystem isolation
- **Union filesystems** → layered images

Technically, containers were now *possible*.

What was missing?
👉 **Developer-friendly tooling**

---

## Chapter 5: The Birth of Docker (2013)

In 2013, Docker appeared.

Docker did **not invent containers**.
Docker **packaged complexity into simplicity**.

Docker gave the world:
- A simple CLI
- Image-based workflows
- Reproducible builds
- Easy sharing via registries

For the first time:
> Developers and Ops spoke the same language.

---

## Chapter 6: “It Works on My Machine” Dies

Docker introduced a powerful idea:

> Build once. Run anywhere.

An application could now be:
- Built on a laptop
- Shipped as an image
- Run unchanged in production

Environment mismatch nearly disappeared.

This changed:
- CI/CD
- DevOps culture
- Microservices adoption

---

## Chapter 7: The Image Becomes the Artifact

Before Docker:
- Code was the artifact

After Docker:
- **The image became the artifact**

Images were:
- Immutable
- Versioned
- Portable
- Reproducible

This aligned perfectly with:
- Infrastructure as Code
- Immutable infrastructure

---

## Chapter 8: The Need for Standards (OCI – 2015)

Docker became wildly popular.
Too popular.

The industry feared:
- Vendor lock-in
- Proprietary container formats

So the **Open Container Initiative (OCI)** was born.

OCI defined:
- How images should look
- How containers should run

This ensured:
- Docker images work everywhere
- Multiple runtimes can coexist

---

## Chapter 9: Containers Everywhere, Chaos Ensues

By 2016:
- Everyone was using containers
- Microservices exploded
- One host was not enough

New problems appeared:
- How do we scale?
- What if a container crashes?
- How do services find each other?
- How do we roll updates safely?

Docker alone was not enough.

---

## Chapter 10: Orchestration Wars

Multiple orchestrators emerged:
- Docker Swarm
- Mesos
- Nomad
- Kubernetes

Kubernetes, inspired by Google’s Borg, won.

Docker adapted:
- Focused on developer experience
- containerd became the runtime
- Docker became Kubernetes-compatible

---

## Chapter 11: The Modern Reality

Today:
- Containers are everywhere
- Docker is the **entry point**
- Kubernetes is the **control plane**
- OCI is the **foundation**
- Linux kernel is the **truth**

Everything else is abstraction.

---

## Final Thought (Very Important)

Containers are not magic.

They are:
- Linux processes
- With isolation (namespaces)
- With limits (cgroups)
- With layered filesystems
- Managed by standards (OCI)

Docker simply told this story **in a way humans could use**.

---

## From Here…

Now that you know *why* Docker exists,
the rest of this file explains *how* it works.

Let’s begin with the fundamentals.
