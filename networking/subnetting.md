---
icon: goal-net
---

# Subnetting

### Subnetting Sheet

* Hosts double each increment of a CIDR
* Always subtract **2** from host total
* **Network ID**: First Address
* **Broadcast**: Last Address

|                         |               |               |      SUBNET | x.0.0.0       |             |            |            |            |
| ----------------------- | ------------- | ------------- | ----------: | ------------- | ----------- | ---------- | ---------- | ---------- |
| CIDR                    | /1            | /2            |          /3 | /4            | /5          | /6         | /7         | /8         |
| Hosts                   | 2,147,483,648 | 1,073,741,824 | 536,870,912 | 268,435,456   | 134,217,728 | 67,108,864 | 33,554,432 | 16,777,216 |
| Class A                 |               |               |      SUBNET | 255.x.0.0     |             |            |            |            |
| CIDR                    | /9            | /10           |         /11 | /12           | /13         | /14        | /15        | /16        |
| Hosts                   | 8,388,608     | 4,194,304     |   4,194,304 | 1,048,576     | 524,288     | 262,144    | 131,072    | 65,536     |
| Class B                 |               |               |      SUBNET | 255.255.x.0   |             |            |            |            |
| CIDR                    | /17           | /18           |         /19 | /20           | /21         | /22        | /23        | /24        |
| Hosts                   | 32,768        | 16,384        |       8,192 | 4,096         | 2,048       | 1,024      | 512        | 256        |
| Class C                 |               |               |      SUBNET | 255.255.255.x |             |            |            |            |
| CIDR                    | /25           | /26           |         /27 | /28           | /29         | /30        | /31        | /32        |
| Hosts                   | 128           | 64            |          32 | 16            | 8           | 4          | 2          | 1          |
|                         |               |               |             |               |             |            |            |            |
| Subnet Mask (Replace X) | 128           | 192           |         224 | 240           | 248         | 252        | 254        | 255        |

### Bits and Octets

#### First Octet

<table data-header-hidden><thead><tr><th width="47.6796875" data-type="number"></th><th width="46.640625" data-type="number"></th><th width="46.60546875" data-type="number"></th><th width="43.53515625" data-type="number"></th><th width="40" data-type="number"></th><th width="40.66796875" data-type="number"></th><th width="43.0078125" data-type="number"></th><th width="43.640625" data-type="number"></th><th></th></tr></thead><tbody><tr><td>128</td><td>64</td><td>32</td><td>16</td><td>8</td><td>4</td><td>2</td><td>1</td><td></td></tr><tr><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>Total: 255</td></tr></tbody></table>

#### Second Octet

<table data-header-hidden><thead><tr><th width="47.6796875" data-type="number"></th><th width="46.640625" data-type="number"></th><th width="46.60546875" data-type="number"></th><th width="43.53515625" data-type="number"></th><th width="40" data-type="number"></th><th width="40.66796875" data-type="number"></th><th width="43.0078125" data-type="number"></th><th width="43.640625" data-type="number"></th><th></th></tr></thead><tbody><tr><td>128</td><td>64</td><td>32</td><td>16</td><td>8</td><td>4</td><td>2</td><td>1</td><td></td></tr><tr><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>Total: 255</td></tr></tbody></table>

#### Third Octet

<table data-header-hidden><thead><tr><th width="47.6796875" data-type="number"></th><th width="46.640625" data-type="number"></th><th width="46.60546875" data-type="number"></th><th width="43.53515625" data-type="number"></th><th width="40" data-type="number"></th><th width="40.66796875" data-type="number"></th><th width="43.0078125" data-type="number"></th><th width="43.640625" data-type="number"></th><th></th></tr></thead><tbody><tr><td>128</td><td>64</td><td>32</td><td>16</td><td>8</td><td>4</td><td>2</td><td>1</td><td></td></tr><tr><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>Total: 255</td></tr></tbody></table>

#### Fourth Octet

<table data-header-hidden><thead><tr><th width="47.6796875" data-type="number"></th><th width="46.640625" data-type="number"></th><th width="46.60546875" data-type="number"></th><th width="43.53515625" data-type="number"></th><th width="40" data-type="number"></th><th width="40.66796875" data-type="number"></th><th width="43.0078125" data-type="number"></th><th width="43.640625" data-type="number"></th><th></th></tr></thead><tbody><tr><td>128</td><td>64</td><td>32</td><td>16</td><td>8</td><td>4</td><td>2</td><td>1</td><td></td></tr><tr><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>Total: 0</td></tr></tbody></table>

#### Result

| Resulting CIDR | Hosts (Exponential) | Hosts           |
| -------------- | ------------------- | --------------- |
| /24            | 2^8                 | 256             |
| (bits on)      | 2^(bits off)        | Resulting hosts |
|                |                     |                 |

Meaning, a **subnet of 255.255.255.0** has **24 bits switched on** (3 sets of octets), **8 bits switched off** (1 set of octets), which gives it **256 hosts available**.

Example: A **Class C Private IP Address network** of **192.168.86.0/24** has a **subnet** of **255.255.255.0**, and has **256 available hosts**. **Subtract 2 hosts** for the **Network ID and  Broadcast address**, leaves us with **254**, So any IP in the range of **192.168.86.1-254** is available to be assigned on that network.
