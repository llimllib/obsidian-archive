---
created: 2024-06-17T23:03:57.382Z
updated: 2024-06-17T23:03:57.382Z
---
```warning
I haven't yet been successful with this!
```

> [!warning] I haven't yet been successful with this


The steps I followed on my mac. [this guide](https://github.com/skyzyx/rg35xx-garlicos-macos-instructions/blob/main/docs/installing-garlicos-single-card.en_us.md) was my main source:

1. acquire microsd card
2. go [here](https://www.patreon.com/posts/garlicos-for-76561333) and download `RG35XX-MicroSDCardImage.7z.001` and `RG35XX-MicroSDCardImage.7z.002`
3. `brew install 7-zip`
4. in the directory where you downloaded the `RG35XX-Micro...` files, run `7zz x RG35XX-MicroSDCardImage.7z.001`
5. insert your microsd card
6. `brew install balenaetcher`
7. Open balena etcher, select the `img` file you created in step 4, and flash it to your microSD card
8. pop out the card and re-insert it, as balena etcher unmounts it when it's done
9. `brew install gdisk`
10. copy the `BIOS` and `CFW` directories from the larger of the two partitions on the disk; we're going to resize and reinstall them later
11. do a whole big `gparted` dance as per the above

I did this, and the machine just won't turn on with the disk in! Back to the drawing board I guess.