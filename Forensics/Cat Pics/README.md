# Cat Pics - Category: Forensics

>New email from cors@nypd.gov:
>
>We were sent a USB to the precinct from someone who claims to be from within the Krypto Foundation, their claim is that it contained leaked messages from within the Company. However it appears to contain unrelated information, it could be a prank, try and make something of it.
>
>Edward Cors - NYPD

I will say, an image with the name "nonsuspiciousimage.png" definitely isn't suspicious at all. Opening the file, we're greeted by an interesting image of a cat. 

![nonsuspiciousimage.png](img/nonsuspiciousimage.png)

There's nothing terribly of note that we can immediately notice. Let's run it through exiftool and see if we've got any interesting metadata.

![Exiftool output on nonsuspiciousimage.png](img/exiftool_output.png)

There's a weird warning about trailer data after the PNG IEND chunk. That means there's data in the image file that goes beyond the actual image data! Let's open it in a hex editor and have a look.

![HxD showing the hex data contained past the IEND chunk](img/HxD_trailer_data.png)

I've highlighted the IEND chunk which shows where the PNG data ends. It looks like there's some weird code at the end of the file including a URL to some page! Let's navigate there and see what we get.

![reallynonsuspiciousimage.jpeg](img/reallynonsuspiciousimage.jpeg)

Seems like we've got another image file. Even less suspcious than the last I might add. If we run this image through exiftool as well...

![ExifTool output on reallynonsuspiciousimage.jpeg](img/exiftool_output2.png)

Does anyone know what "CONFIDENTIAL DO NOT SHARE" means? Anyway, we can see the flag! Actually, we can see it three times funnily enough.

**Flag:** magpieCTF{p1ctur36_In_PicTuR37}
