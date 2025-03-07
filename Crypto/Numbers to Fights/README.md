# Numbers to Fights - Category: Crypto

>Christina Krypto's Diaries:
>
>"Professor Richard Hash believes that cryptography should remain rigid and bound by outdated principles, and he sees my innovations as a threat to his traditional methods. But what he doesn't understand is that the world is evolving. Numbers alone aren’t enough to protect our digital communication anymore—they can be left vulnerable.The future of cryptography is about moving beyond the constraints of the past, and I’m leading the way."

The provided `output.txt` contains a very loooooong number.

```12665394834264763794106437036616675274345928889080203342691794650101329828215165```

Other than that, there isn't any other information so we'll have to find the flag just from this. It (probably) can't be encrypted with any kind of cipher (at least none that requires a key like RSA) since this is all we got. 

It seems to just be a decimal (base 10) number from the looks of it. My first thought is that maybe if we split the digits up into groups of two, the digits will represent ASCII characters. So the first two digits are 12, then 66, 53, etc. But that quickly doesn't really make sense since the ASCII character 12 is not an actual printing character if you look on an ASCII table. So we'll have to dig a little deeper than that.

Another thought. Perhaps we're on the right track but we're using the **wrong base**. The idea is if we turn this number into base-2 and then seperate it into groups of 8 digits (8 bits is 1 byte), maybe then the bytes will then form some text. Each byte can be translated into its corresponding ASCII character. Instead of doing it by hand, we can use a very simple python script to read the number, turn it into its byte representation, and print it out.

```python
with open("output.txt", "r", encoding="utf-8") as f:
    the_number: int = int(f.read().strip())

# The 33 represents the number of bytes to convert the given number into. 
# We can guess some arbitrary numbers if we don't know what it would be. 
# Putting more than 33 will just result in some padding being placed around the flag.
the_bytes: bytes = the_number.to_bytes(33)
print(the_bytes)
```

Output: `b'magpieCTF{numb3r_t0_t3xt_1s_34sy}'`

Printing out the output, we get the flag! When printing, Python will very helpfully turn the bytes into ASCII text to show on the screen, if it can.

**Flag:** magpieCTF{numb3r\_t0\_t3xt\_1s\_34sy}
