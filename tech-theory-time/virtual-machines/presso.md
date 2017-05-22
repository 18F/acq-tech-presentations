class: left, top
# Virtual machines (VM)
little computers inside your computer

---

### What's a real computer?

* hardware - motherboard, processor, RAM, storage, video, USB
* bootstrap firmware - super low-level software that starts up the hardware; BIOS, UEFI
* operating system (OS) - lowest user-level software; Windows, MacOS, Linux
* applications - Slack, Chrome, Atom

---

### Booting a computer

1. power comes in and all the hardware turns on
2. firmware embedded in the hardware controls how it starts up
3. once the necessary components report that they're ready, the motherboard tells the
processor to start executing from the boot sector of the primary storage device (hard drive)
4. the operating system controls what's in the boot sector, so at this point it takes over
5. the OS has drivers that tell it how to talk directly to the hardware; it uses those to
turn on video, hook up the keyboard, etc.

???
1. On in the way that a lightbulb is on, not in the way that a computer is "on"
2. 
3. computer is on in a computery way

---

### Virtual computers

There are two kinds of virtual machines:

# Emulated

# Virtualized

---

### Virtual machine / .white[Quick terms]

* **Host**
> The real computer

* **Guest**
> The virtual computer

* **Hypervisor**
> Software on a host that is responsible for running guest computers

---

### Virtual machine / .white[Emulation]

In an emulation VM, an .highlight[application] pretends to be hardware.  It tells the
.highlight[guest OS] to start executing, and when the guest OS tries to interact with
the hardware, it is actually interacting with the application.  The application then
translates those interactions into commands on the .highlight[host OS] to achieve what
the guest is trying to do.

.loud[Example:] A Nintendo emulator application running on your Mac
(.highlight[would be illegal]) pretends to be a MOS 6502 microchip.  The Nintendo
guest tells the emulated 6502 to play a sound.  The host then decodes
that and uses it to tell your Mac to play a sound.

---

### Virtual machine / .white[Emulation]

Emulation is soooooo slow, y'all.  Really, painfully slow sometimes.  Everything the
guest wants to do has to be decoded and translated from the pretend hardware into
something the host OS understands.

It's fine to emulate really simple computers (like the NES), but it's
.highlight[practically impossible] to emulate more complex computers (like your laptop).

.loud[But we're still doing it with modern devices.] Developing software for Android
devices requires using an emulator. It's one of the most frustrating parts of doing
Android development!

???
There are advantages to emulation, though.  A proper emulator will nearly exactly match
the hardware it is emulating, including weird bugs and quirks.  That can actually make
it easier to find bugs in your software, oddly enough.  But that's why Android still
uses emulation.

---

### Virtual machine / .white[Virtualization]

In a virtualized VM, the guest OS has its own access to the host hardware.  A hypervisor
on the host (e.g., .highlight[Virtualbox], .highlight[VMWare], .highlight[Parallels])
controls the guest's access to the host hardware.

* how much memory can it use
* how much processor time can it use
* whether it can directly interact with USB devices
* etc.

---

### Virtual machine / .white[Virtualization]

The hypervisor essentially pokes a hole through the host OS directly to the hardware
and lets the guest machine access the hardware through that controlled mechanism.

The guest is .highlight[isolated] from the host.  The guest can't access
memory or storage that hasn't been specifically set aside for it.  The guest can't
see the host's network activity.

The host can still see everything, but in practice hosts generally don't peak into
guests except to figure out problems.
