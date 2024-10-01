<img src="https://github.com/kichkiro/42_cursus/blob/assets/banner_netpractice2.jpg?raw=true" width="100%"/>

# Net Practice

<i>
    <p>
        This project is a general practical exercise to let you discover networking.
    </p>
</i>

#### <i>[subject](_subject/en.subject.pdf) v.2</i>

<details>
<summary><i><b>Project Structure  📂</b></i></summary>

``` js
├── README.md
├── LICENSE
├── _notebook
│   └── ipv4_calculator.ipynb
├── _subject
│   ├── en.subject.pdf
│   └── net_practice.1.4.tgz
└── project
    ├── level1.json
    ├── level2.json
    ├── level3.json
    ├── level4.json
    ├── level5.json
    ├── level6.json
    ├── level7.json
    ├── level8.json
    ├── level9.json
    └── level10.json
```
</details>

## 📌 - Key Topics

### TCP/IP Addressing
TCP/IP addressing forms the backbone of modern network communication. 

This project focuses on gaining a practical understanding of IP addresses, subnet masks, routers, and how they interact within a network to facilitate communication between devices.

## 📈 - [IPv4 Calculator](_notebook/ipv4_calculator.ipynb)

### Network Address

Calculate the network address from the IP address and netmask.

- Step 1: Write the given IP address in binary format.

- Step 2: Write the subnet mask in binary form.

- Step 3: Perform the logical  ANDing operation between the corresponding octets of the IP address and the subnet mask.

- Step 4: Convert the result back to the decimal format and this will be the network address.


```python
# IP Address ----------------------------------------------------------------->
ip_addr = input("IP Address [xxx.xxx.xxx.xxx]: ")
ip_addr_b = " ".join("{:08b}".format(int(byte)) for byte in ip_addr.split("."))

# Netmask -------------------------------------------------------------------->
netmask = int(input("Netmask [CIDR notation]: "))
netmask_b = "".join('1' if i < netmask else '0' for i in range(32))
netmask_b = " ".join(netmask_b[i:(i + 8)] for i in range(0, 32, 8))

# Network Address ------------------------------------------------------------>
network_addr_bin = "".join(str(int(ip_addr_b[i]) & int(netmask_b[i])) if 
    ip_addr_b[i] != " " else " " for i in range(35))
network_addr = "".join(str(int(byte, 2)) + "." for byte in 
    network_addr_bin.split(" ")).strip(".")

# Visualization -------------------------------------------------------------->
print(
	f"IP Address         {ip_addr_b} -> {ip_addr}\n"
	f"                                   AND\n"
	f"Netmask            {netmask_b} -> /{netmask}\n"
	f"                   -----------------------------------\n"
	f"Network Address    {network_addr_bin} -> {network_addr}/{netmask}"
)
```

    IP Address         10100111 11110001 00101010 00010101 -> 167.241.42.21
                                       AND
    Netmask            11111111 11111111 11111111 11111000 -> /29
                       -----------------------------------
    Network Address    10100111 11110001 00101010 00010000 -> 167.241.42.16/29


### Broadcast Address

Calculate broadcast address from the network address.

- Step 1: replace all bits dedicated to hosts with 1.


```python
# Network Address ------------------------------------------------------------>
network = input("Network Address [xxx.xxx.xxx.xxx/xx]: ")
netmask = int(network[-2:])
network_addr = network[:-3]
network_addr_b = "".join("{:08b}".format(int(byte)) for byte in 
    network_addr.split("."))

# Broadcast Address ---------------------------------------------------------->
broadcast_addr_b = network_addr_b[:netmask] + '1' * (32 - netmask)
broadcast_addr = ".".join(str(int(broadcast_addr_b[i:i+8], 2)) for i in 
    range(0, 32, 8))

# Visualization -------------------------------------------------------------->
def add_spaces(string):
    return ' '.join(string[i:i + 8] for i in range(0, 32, 8))

print(
	f"Network Address    {add_spaces(network_addr_b)} -> {network}\n"
	f"                   -----------------------------------\n"
	f"Broadcast Address  {add_spaces(broadcast_addr_b)} -> {broadcast_addr}"
)
```

    Network Address    10100111 11110001 00101010 00010000 -> 167.241.42.16/29
                       -----------------------------------
    Broadcast Address  10100111 11110001 00101010 00010111 -> 167.241.42.23


### Host Addresses

Valid host addresses are those all between the network address and the broadcast address.


```python
# Network Address ------------------------------------------------------------>
network = input("Network Address [xxx.xxx.xxx.xxx]: ")

# Broadcast Address ---------------------------------------------------------->
broadcast = input("Broadcast Address [xxx.xxx.xxx.xxx]: ")

# Hosts Addresses ------------------------------------------------------------>
print(f"Host min -> {network} + 1\nHost max -> {broadcast} - 1")
```

    Host min -> 167.241.42.16 + 1
    Host max -> 167.241.42.23 - 1

## ⚖️ - License 

See [LICENSE](https://github.com/kichkiro/42_cursus/blob/main/LICENSE)
