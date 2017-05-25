class: left, top
# Virtual machines (VM)
little computers inside your computer

---

### What's a real computer?

* hardware - motherboard, processor, RAM, storage, video, USB
* operating system (OS) - lowest user-level software; Windows, MacOS, Linux
* applications - Slack, Chrome, Atom

---

### What's a real computer?

<table>
  <tr class="apps">
    <td>Slack</td>
    <td>Chrome</td>
    <td>Atom</td>
    <td>apps...</td>
  </tr>
  <tr class="os">
    <td colspan="4">operating system (Windows, macOS, Linux)</td>
  </tr>
  <tr class="hardware">
    <td colspan="4">hardware (processor, memory)</td>
  </tr>
</table>

---

### Virtual machines

# .white[A virtual machine is logically an entire computer]

It just runs on .highlight[virtual] hardware

---

### Virtual machines / .white[virtual hardware]

> &ldquo;Not physically existing but made by software to appear to do so&rdquo;

--
count: false

Software applications can manage the way other applications can use the hardware.
As far as the second application can tell, it's using the hardware directly, but
in fact, the first application is managing how it uses the hardware.  The first
application has created .highlight[virtual hardware].

--
count: false

The applications that create virtual hardware for virtual machines are called
.highlight[hypervisors]. It's a weird word.

--
count: false

The *how* is really complicated.  We won't go there.

---

### Virtual machines

<table>
  <tr class="apps">
    <td>app</td>
    <td>app</td>
    <td>app</td>
    <td rowspan="3" style="background: transparent; color: white;">⬅ vm</td>
  </tr>
  <tr class="os">
    <td colspan="3">guest operating system</td>
  </tr>
  <tr class="hardware">
    <td colspan="3">virtual hardware</td>
  </tr>
  <tr class="apps">
    <td colspan="3">hypervisor</td>
    <td>apps...</td>
  </tr>
  <tr class="os">
    <td colspan="4">host operating system</td>
  </tr>
  <tr class="hardware">
    <td colspan="4">hardware</td>
  </tr>
</table>

---

### Virtual machines

A virtual machine runs on virtual hardware, created and managed by the .highlight[host]
machine.  That means the host controls the .highlight[guest's] access.

* how much memory it can access
* how much processor time it can use
* which files it can see
* etc.

When a "real" computer is also running virtual machines, we refer to the
"real" computer as the .loud[host].  The virtual machines are called
.loud[guests].

---

### Virtual machines

The .highlight[hypervisor] essentially pokes a hole through the host OS directly to the hardware
and lets the guest machine access the hardware through that controlled mechanism.

The guest is .highlight[isolated] from the host.  The guest can't access
memory or storage that hasn't been specifically set aside for it.  The guest can't
see the host's network activity.

The host can still see everything, but in practice hosts generally don't peak into
guests except to figure out problems.

---

### Virtual machines / .white[the cloud]

## .white[Most of the computers in the cloud are virtual machines]

Using virtual machines, cloud providers can turn a fixed amount of hardware into a
variable number of computers.  They can add computers as needed without necessarily
having to add hardware.

And they can rely on the hypervisors to automate a lot of the creation process.  Many
data centers are heavily automated, to the point that creating a new virtual machine
often takes less than a minute.

---

### Containers

There are other kinds of virtualization, like containers (these are what
.highlight[Docker] creates).  Containers are *not* entire virtual computers.

Containers use what is called "operating system virtualization" instead of
hardware virtualization like virtual machines use.

## The host shares its operating system into the container

---

### Containers

<table>
  <tr class="apps">
    <td>app</td>
    <td>app</td>
    <td>app</td>
    <td rowspan="2" style="background: transparent; color: white;">⬅ container</td>
  </tr>
  <tr class="hardware">
    <td colspan="3">container image</td>
  </tr>
  <tr class="apps">
    <td colspan="3">container manager</td>
    <td>apps...</td>
  </tr>
  <tr class="os">
    <td colspan="4">host operating system</td>
  </tr>
  <tr class="hardware">
    <td colspan="4">hardware</td>
  </tr>
</table>

The .highlight[container image] keeps track of any changes the container makes to the
operating system, but it _only_ stores the changes. Those changes are only visible to
the container and don't affect the host!

---

### Containers / .white[advantages over VMs]

* because they use the host's operating system, they turn on instantly - no boot-up
* they also don't need as much storage or memory because they use the host's operating system
* generally they only run a single application
* they don't need much configuration - they inherit it from the host operating system
