Mifare Tags work on [13.56Mhz](https://en.wikipedia.org/wiki/MIFARE) 
# Mifare Classic 1k 

## IOS
as it appears IOS [does not](https://forums.developer.apple.com/forums/thread/133179) support reading of Mifare Classic 1K cards. You can use an external reader to still read them but it does not work out of the box as it does under android. Other Mifare standarts [seem supported](https://developer.apple.com/documentation/corenfc/nfcmifaretag). 


# Mifare Ultralight C 

## Sources
- [fact sheet](https://www.nxp.com/docs/en/fact-sheet/MIFARE-ULTRALIGHT-C-FS.pdf)
- [product sheet](https://www.nxp.com/docs/en/data-sheet/MF0ICU2.pdf)


## Security 

- 3DES Authentication 
- "Anti cloning support" by unique 7 byte Serial number for each device
- ...


### looking into breaking the security of these tags

what we currently have : we have a reader 