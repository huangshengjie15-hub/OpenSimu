# OpenSimu

[简体中文](README.md) · **English** · [日本語](README.ja.md)

OpenSimu is an open-source project for lightweight network simulation. Its goal is to let network researchers build a small topology on a personal computer, change a device configuration, observe how packets are forwarded, and share the experiment so others can reproduce it.

The project is in the planning stage. We’re starting with Huawei and Cisco routers. We plan to model interfaces, configuration commands, and routing behavior for specific device models and network OS versions. Each implementation will point to the relevant section of a public vendor manual and include a reproducible experiment.

## Testing static routes between two routers

If you remove just one route from R1, can the hosts still ping each other? This is the first experiment we want OpenSimu to reproduce.

```text
PC-A ─── R1 (Huawei) ─── R2 (Cisco) ─── PC-B
```

1. Assign a separate IPv4 subnet to each link. Set each host’s default gateway to its local router.
2. On each router, add a static route to the remote LAN with the other router as the next hop. A `ping` from either host to the other should succeed.
3. Remove R1’s static route to PC-B’s LAN. The entry should disappear from R1’s routing table. If R1 has no default or alternate route, `ping` should fail in both directions. Even if PC-B’s request reaches PC-A, its reply has no path back through R1.

We plan to follow this lab with experiments on VLAN isolation and dynamic route learning with OSPF.

## Contributing

Have a device behavior you’d like to reproduce? Open an issue with the **device model and OS version**, a **link to the relevant manual section**, and the **smallest topology and configuration** that demonstrate the behavior. Describe the expected result. If you’ve tested it, a routing table or command transcript you have permission to publish can help others check their results. [Suggest an experiment](https://github.com/huangshengjie15-hub/OpenSimu/issues)

For model-specific documentation, start with the vendors’ own resources. [Huawei NetEngine AR Knowledge Base](https://info.support.huawei.com/network/ptmngsys/Web/5G_AR/en/index.html) · [Cisco router support](https://www.cisco.com/c/en/us/support/routers/category.html)

## License

OpenSimu uses the Apache License 2.0, which permits commercial use. When redistributing the software, include a copy of the license, mark files you have modified, and retain applicable copyright and attribution notices as required by the license. Vendor manuals are subject to their own terms. [Read the license](LICENSE)
