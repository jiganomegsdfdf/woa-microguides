# Half-noob guide "How-To add I2C node into XBL DT?"
#### To check "almost always" values - look at the other present nodes in your XBL DT.
---
1. To get **"@*"** - open mainline [.dtsi](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/arch/arm64/boot/dts) for device and search for i2c node by searching page for **"@<core_base_addr + core_offset>"**, then look for parent of this i2c node and count his children from 0 to your node **(including your node)**
<br>Also, name of your node will be i2c_device_config_**"Same number as reg/@**
2. To get **"reg"** - you need to look at number after **"@"** in your **i2c_device_config_*** node
---
3. To get **"qupv3_instance"** - you need to look at **core_base_addr**, 
<br>**0x900000** = 0,
<br>**0xA00000** = 1,
<br>**0x800000** = 2.
---
4. **core_index** value is same as **reg/@**
5. To get **se_index** - look at <strong>S*</strong> number inside of **se_clock**, where * - some number
6. To get **gpi_index** - you can only use one-by-one method, from 0 to any number
---
7. **core_irq** almost always = **00**
8. **polled_mode** almost always = **01**
9. **min_data_length_for_dma** almost always = **00**
---
10. To get **i2c_hub** - look for another **i2c_device_config** in device tree with same **core_base_addr** parameter, and take it from there.
---
11. To get **scl_encoding** - open mainline [.dtsi](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/arch/arm64/boot/dts) for device and look at **pinctrl-0** parameter of i2c node that you can find by searching page for **@<core_base_addr + core_offset>**, then you copy something like **hub_i2c5_data_clk** and search 
page for it, you will find node with same name, then you look at **pins** parameter and take number after **gpio** after **","**
then take this [Python Script](https://gist.github.com/jiganomegsdfdf/92adce678a69126dcf5699d0fafff1e3) and run it, paste this number **(only number)** into script when it ask for it and press enter.
12. To get **sda_encoding** - follow same steps as **scl_encoding**
---
13. **tcsr_reg_offset** almost always = **0x00**
14. **tcsr_base_addr** almost always = **0x1fc0000**
15. **tcsr_reg_value** almost always = **0x00**
---
16. To get **se_clock** - open mainline [.dtsi](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/arch/arm64/boot/dts) for device and look at **clocks** parameter of i2c node that you can find by searching page for **@<core_base_addr + core_offset>**, 
then find one of them that have <strong>S*</strong> in his text, where * - some number, just copy-paste it and make it lowercase.
