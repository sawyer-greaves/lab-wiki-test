[Home](Home)
# Lab Network Drive (Group Drive)

The lab has a network drive to store files generated for research conducted by the lab.

## Usage Standards

- Use Handbrake to reduce video file size when putting them on the group drive

---
## Mapping/Mounting the Lab Network Drive (Group Drive)

### Windows

### Linux
    - https://wiki.ubuntu.com/MountWindowsSharesPermanently
    - `//chips.eng.utah.edu/telerobotics /home/adam/telerobotics-group cifs credentials=/home/adam/.smbcredentials,uid=adam,gid=adam,vers=2.0 0 0`
    - https://serverfault.com/questions/222074/fstab-and-cifs-mounting-possible-to-store-authentication-information-outside-of
    - https://askubuntu.com/questions/1262419/safer-alternative-to-using-smbcredentials
    - https://askubuntu.com/questions/1027271/secure-password-when-mounting-the-file-server-using-smbcredentials/1081421#1081421