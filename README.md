# MD5_Colission_Attack_Lab

Instruction: https://seedsecuritylabs.org/Labs_16.04/PDF/Crypto_MD5_Collision.pdf

### Task 1

Generate a prefix.txt containing 64 ```'9'```:


python3 -c "print('9'*64,end='')" > prefix.txt
ls -ld prefix.txt

Use it to create 2 files with the same MD5 value:

```md5collgen -p prefix.txt -o out1.bin out2.bin```

Wait for seconds, check if the 2 files are different:

```$ diff out1.bin out2.bin
Binary files out1.bin and out2.bin differ```

Check if their MD5 values are the same:

```$ md5sum out1.bin
b3d3a557001d81af72250f58b1cea4aa  out1.bin
$ md5sum out2.bin
b3d3a557001d81af72250f58b1cea4aa  out2.bin```

4aa  out2.bin
Compare their differences:

```$ hexdump out1.bin > hex1
$ hexdump out2.bin > hex2
$ diff hex1 hex2
4,6c4,6
< 0000050 3d59 83f8 861b 0b01 523e 813f a5f3 9c8c
< 0000060 0412 b9f9 0e70 0fbd 508b 4256 a7ee 3f38
< 0000070 d438 668f 4abb ed3e 9003 ab89 a859 58bd
---
> 0000050 3d59 03f8 861b 0b01 523e 813f a5f3 9c8c
> 0000060 0412 b9f9 0e70 0fbd 508b 4256 27ee 3f39
> 0000070 d438 668f 4abb ed3e 9003 2b89 a859 58bd
8,10c8,10
< 0000090 7dac 713e e61b 6a1e 1acb 3d6e 86ec e602
< 00000a0 7c98 5b26 ca06 3fde 4c8a 973c 2450 28ea
< 00000b0 f128 b84a 6c42 0ac2 db2d 0427 baa5 93b1
---
> 0000090 7dac f13e e61b 6a1e 1acb 3d6e 86ec e602
> 00000a0 7c98 5b26 ca06 3fde 4c8a 973c a450 28e9
> 00000b0 f128 b84a 6c42 0ac2 db2d 8427 baa5 93b1```

Use the program diff_bytes.py to find out where they differs from each other in the last 128 bytes:

```head -c 128 out1.bin > P
head -c 128 out2.bin > Q
diff_bytes.py P Q```
