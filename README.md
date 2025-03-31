# **Writeup: Chinese Cipher Challenge**  
**Category**: Cryptography  
**Points**: 100  
**Solves**: 0/5.  

## **Initial Observations**  
We are given an unusual ciphertext:  
```
籀簿 簼簿 籂簿 籮簻 籂簻 簾簽 籂簿 籮簻 籭簿 簾簽 籮簿 籫簻 簺簿 籂簾 籀簾 簾簾
```  
At first glance, it appears to be Chinese characters, but each "word" consists of exactly two characters—an unusual pattern that suggests encoding rather than natural language.  

## **Decryption Process**  

### **Step 1: ROT8000 Decoding**  
After experimenting with various decryption methods (including Unicode-based approaches), we applied **ROT8000**—a rotational cipher that shifts Unicode characters by 8000 positions.  

The result was a hexadecimal string:  
```
76 36 96 e2 92 54 96 e2 d6 54 e6 b2 16 95 75 55
```  
![Image](https://github.com/user-attachments/assets/50b97747-a0a3-4ced-bd63-12087f4c6306)

### **Step 2: Hex Decoding & Reversing**  
Directly decoding the hex produced garbled output:  
```
v6âTâÖTæ²uU
```
![Image](https://github.com/user-attachments/assets/6a0a8fa8-5510-4c21-989f-b7878a3bb4f5)

However, reversing the hex string before decoding yielded a more structured result:  

```
UWYa+nEm.iE).icg
```
![Image](https://github.com/user-attachments/assets/111826d3-ff95-4052-a0b2-c678f78cc151)

This hinted at further encoding, possibly involving XOR encryption.  

### **Step 3: XOR Brute-Force Attack**  
Since we lacked an obvious key, we performed a **XOR brute-force attack**. After testing several keys, we discovered that XORing with `1a` produced the flag:  

**Final Output:**  
```
OMC{1t_w4s_34sy}
```
![Image](https://github.com/user-attachments/assets/d333e793-6d78-43e7-bf09-f962c413aec9)

## **Conclusion**  
The challenge involved:  
1. **ROT8000 decoding** to reveal a hex string.  
2. **Reversing the hex** to expose a partially readable message.  
3. **XOR brute-forcing** to uncover the flag.  

### **Automated Solution (CyberChef)**  
For a step-by-step breakdown, see this [**CyberChef recipe**](https://gchq.github.io/CyberChef/#recipe=ROT8000()Reverse('Character')From_Hex('Auto')XOR_Brute_Force(1,100,0,'Standard',false,true,false,'')&input=57GA57C/IOewvOewvyDnsYLnsL8g57Gu57C7IOexguewuyDnsL7nsL0g57GC57C/IOexruewuyDnsa3nsL8g57C%2B57C9IOexruewvyDnsavnsLsg57C657C/IOexguewviDnsYDnsL4g57C%2B57C%2B).  

![Final Decoding Steps](https://github.com/user-attachments/assets/ce5ae93d-850e-4457-a040-c7636158f4f8)  

---

### **Flag**  
**`OMC{1t_w4s_34sy}`**  
