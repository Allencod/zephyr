:orphan:

.. _zephyr_1.14:

Zephyr Kernel 1.14.0 (Working Draft)
####################################

We are pleased to announce the release of Zephyr kernel version 1.14.0.

Major enhancements with this release include:

* TBD

The following sections provide detailed lists of changes by component.

Security Vulnerability Related
******************************

The following security vulnerabilities (CVEs) were addressed in this release:

* Tinycrypt HMAC-PRNG implementation doesn't take the HMAC state
  clearing into account as it performs the HMAC operations, thereby using a
  incorrect HMAC key for some of the HMAC operations.
  CVE-2017-14200

* The shell DNS command can cause unpredictable results due to misuse of stack
  variables.
  CVE-2017-14201

* The shell implementation does not protect against buffer overruns resulting
  in unpredictable behavior.
  CVE-2017-14202

* We introduced Kernel Page Table Isolation, a technique for
  mitigating the Meltdown security vulnerability on x86 systems. This
  technique helps isolate user and kernel space memory by ensuring
  non-essential kernel pages are unmapped in the page tables when the CPU
  is running in the least privileged user mode, Ring 3. This is the
  fix for Rogue Data Cache Load (CVE-2017-5754).

* We also addressed these CVEs for the x86 port:

  - Bounds Check Bypass (CVE-2017-5753)
  - Branch Target Injection (CVE-2017-5715)
  - Speculative Store Bypass (CVE-2018-3639)
  - L1 Terminal Fault (CVE-2018-3620)
  - Lazy FP State Restore (CVE-2018-3665)

Kernel
******

* TBD

Architectures
*************

* TBD

Boards & SoC Support
********************

* TBD

* Added the all new :ref:`NRF52 simulated board <nrf52_bsim>`:
  It models some of the HW in an NRF52832 SOC, to enable running
  full system, multinode simulations, without the need of real HW.
  Enabling fast, reproducible tests, development and debugging of the
  application, BT stack and kernel. It relies on `BabbleSim`_
  to simulate the radio physical layer.

.. _BabbleSim:
   https://BabbleSim.github.io

Drivers and Sensors
*******************

* TBD

* Added new drivers and backends for :ref:`native_posix <native_posix>`:

  - An UART driver which maps the Zephyr UART to a new host PTY
  - A USB driver which can expose a host connected USB device
  - A display driver which will render to a dedicated window using the SDL
    library
  - A dedicated backend for the new logger subsystem

Networking
**********

* The :ref:`BSD socket API <bsd_sockets_interface>` should be used by
  applications for any network connectivity needs.
* Majority of the network sample applications were converted to use
  the BSD socket API.
* New BSD socket based APIs were created for these components and protocols:

  - :ref:`MQTT <mqtt_socket_interface>`
  - :ref:`CoAP <coap_sock_interface>`
  - :ref:`LWM2M <lwm2m_interface>`
  - :ref:`SNTP <sntp_interface>`
* net-app client and server APIs were removed. This also required removal of
  the following net-app based legacy APIs:

  - MQTT
  - CoAP
  - SNTP
  - LWM2M
  - HTTP client and server
  - Websocket
* Network packet (:ref:`net-pkt <net_pkt_interface>`) API overhaul. The new
  net-pkt API uses less memory and is more streamlined than the old one.
* Implement following BSD socket APIs: ``freeaddrinfo()``, ``gethostname()``,
  ``getnameinfo()``, ``getsockopt()``, ``select()``, ``setsockopt()``,
  ``shutdown()``
* Converted BSD socket code to use global file descriptor numbers.
* Network subsystem converted to use new :ref:`logging system <logger>`.
* Added support for disabling IPv4, IPv6, UDP, and TCP simultaneously.
* Added support for :ref:`BSD socket offloading <net_socket_offloading>`.
* Added support for long lifetime IPv6 prefixes.
* Added enhancements to IPv6 multicast address checking.
* Added support for IPv6 Destination Options Header extension.
* Added support for packet socket (AF_PACKET).
* Added support for socket CAN (AF_CAN).
* Added support for SOCKS5 proxy in MQTT client.
* Added support for IPSO Timer object in LWM2M.
* Added support for receiving gratuitous ARP request.
* Added :ref:`sample application <google-iot-mqtt-sample>` for Google IoT Cloud.
* :ref:`Network interface <net_if_interface>` numbering starts now from 1 for
  POSIX compatibility.
* :ref:`OpenThread <thread_protocol_interface>` enhancements.
* :ref:`zperf <zperf-sample>` sample application fixes.
* :ref:`LLDP <lldp_interface>` (Link Layer Discovery Protocol) enhancements.
* ARP cache update fix.
* gPTP link delay calculation fixes.
* Changed how network data is passed from
  :ref:`L2 to network device driver <network_stack_architecture>`.
* Removed RPL (Ripple) IPv6 mesh routing support.
* Network device driver additions and enhancements:

  - Added Intel PRO/1000 Ethernet driver (e1000).
  - Added SMSC9118/LAN9118 Ethernet driver (smsc911x).
  - Added Inventek es-WiFi driver for disco_l475_iot1 board.
  - Added support for automatically enabling QEMU based Ethernet drivers.
  - SAM-E70 gmac Ethernet driver Qav fixes.
  - enc28j60 Ethernet driver fixes and enhancements.

Bluetooth
*********

* TBD
* Done several fixes for big endian architectures

Build and Infrastructure
************************

* TBD
* Added support for out of tree architectures
* `BabbleSim`_ has been integrated in Zephyr's CI system.

Libraries / Subsystems
***********************

* TBD

HALs
****

* TBD

Documentation
*************

* Reorganized subsystem documentation into more meaningful collections
  and added or improved introductory material for each subsystem.
* Overhauled  Bluetooth documentation to split it into
  manageable units and included additional information, such as
  architecture and tooling.
* Added to and improved documentation on many minor subsystems and APIs
  including socket offloading, Ethernet management, LLDP networking,
  network architecture and overview, net shell, CoAP, network interface,
  network configuration library, DNS resolver, DHCPv4, DTS, and more.
* Introduced a new debugging guide that documents all the different
  variations of debug probes and host tools in
  one place, including which combinations are valid.
* Clarified and improved information about the west tool and its use.
* Improved development process documentation including how new features
  are proposed and tracked, and clarifying API lifecycle, issue and PR
  tagging requirements, contributing guidelines, doc guidelines,
  release process, and PR review process.
* Introduced a developer "fast" doc build option to eliminate
  the time needed to create the full kconfig option docs from a local
  doc build, saving five minutes for a full doc build.
* Made dramatic improvements to the doc build processing, bringing
  iterative local doc generation down from over two minutes to only a
  few seconds. This makes it much faster for doc developers to iteratively
  edit and test doc changes locally before submitting a PR.
* Added a new ``zephyr-file`` directive to link directly to files in the
  Git tree.
* Introduced simplified linking to doxygen-generated API reference
  material.
* Made board documentation consistent, enabling a board-image carousel
  on the zephyrproject.org home page.
* Reduced unnecessarily large images to improve page load times.
* Added CSS changes to improve API docs appearance and usability
* Made doc version selector more obvious, making it easier to select
  documentation for a specific release
* Added a friendlier and more graphic home page.

Tests and Samples
*****************

* TBD
* A new set of, multinode, full system tests of the BT stack,
  based on `BabbleSim`_ have been added.

Issue Related Items
*******************

These GitHub issues were addressed since the previous 1.13.0 tagged
release:

.. comment  List derived from GitHub Issue query: ...
   * :github:`issuenumber` - issue title

* :github:`99999` - issue title
