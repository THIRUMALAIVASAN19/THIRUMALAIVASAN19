## Hi there 👋

<!--
**THIRUMALAIVASAN19/THIRUMALAIVASAN19** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
-->
In C, bitwise operations allow direct manipulation of individual bits within a byte, word, or register. These operations are performed using the following operators:

| → Bitwise OR — typically used to set a bit
& → Bitwise AND — used to clear or check a bit
^ → Bitwise XOR — used to toggle (invert) a bit
~ → Bitwise NOT — used to flip all bits (1 to 0, 0 to 1)
<<,  >> → Bit shift left/right — used to move bit positions
 
Common bit-masking patterns:

reg |= (1 << n);     // Set bit n
reg &= ~(1 << n);    // Clear bit n
reg ^= (1 << n);     // Toggle bit n
if (reg & (1 << n))  // Check if bit n is setCopy
These operations are used to target and modify only specific bits, without disturbing others.

8-bit Visualization Example
Bit	7	6	5	4	3	2	1	0
Value	128	64	32	16	8	4	2	1
E.g.

To set bit 3 → reg |= (1 << 3)
To clear bit 6 → reg &= ~(1 << 6)
To check bit 0 → reg & (1 << 0)
To toggle but 3 → reg ^= (1 << 3)
32-bit Register Usage
Bitwise techniques apply the same way for uint32_t types — often used in 32-bit MCUs for status/configuration registers.

Example:

ctrl_reg |= (1U << 23); // Set bit 23 in a 32-bit control register

 

Common Pitfalls (Practical Tips)
Forgetting parentheses: 1 << n must be inside parentheses during masking:
 ✅ reg |= (1 << 4) vs ❌ reg |= 1 << 4 & 0xF
Using signed types: Never use int for register work — use uint8_t, uint16_t, or uint32_t.
 Signed values may cause undefined behavior when shifting, as MSB (Most Significant Bit) used for sign.
Wrong shift width: Shifting more than the data type width (e.g. 1 << 32 on a 32-bit int) is undefined.
Accidental overwrite:
reg = (1 << 2); // WRONG: overwrites entire register  
reg |= (1 << 2); // RIGHT: sets only the 2nd bitCopy
Check before toggle: Be careful when toggling flags — you may unintentionally clear a set flag.
 
Relevance in Embedded/Firmware
All MCU peripherals are controlled via register bits — timers, GPIOs, UART, ADC, interrupts, etc.
Bit masking ensures safe modification without overwriting unrelated fields.
Used in flags, control masks, interrupt status checks, and power/clock configuration.
