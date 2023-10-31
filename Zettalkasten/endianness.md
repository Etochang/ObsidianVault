202310211635
Meta Tags: #concept  
Tags: [[computer architecture]] [[computer science]]

# endianness

is a way of representing multi-[[byte]] [[data type|data types]] in [[memory]]. 

## 2 Types of Endianness

### 1. Big-Endian (BE)

The [[MSB]] is stored at the lowest [[memory address]], while the [[LSB]] is stored at the highest.

For example, `0x12345678` would be stored like:
```
Address:   0x1000   0x1001   0x1002   0x1003
Value:     0x12     0x34     0x56     0x78
```
### 2. Little-Endian (LE)

Vice-versa to BE. 

Same value would be stored like:
```
Address: 0x1000 0x1001 0x1002 0x1003 
Value:   0x78   0x56   0x34   0x12
```

---
# *References*
https://chat.openai.com/share/9637ce1d-4ced-4189-9941-d95369c7b2fc