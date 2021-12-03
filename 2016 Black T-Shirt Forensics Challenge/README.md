# 2016 Black T-Shirt Forensics Challenge ![Dragon Eye Intelligence][DEI]
[DEI]:https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/fdb3456cadce1303e2183c607c3688c0f82f0bb3/imgs/badge.png

### Setup
<p align="center">
    To download the challenge files (and case ingests) yourself, download the folders above and extract the zip.part files with a compatible zip extractor (7-zip). Afterwards check all of the file hashes to ensure they have not been modified.
</p>

<br />

<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/7b8983266033500a25e3381b96612046c2a1d507/imgs/certutil-MD5.png" align="right"
     alt="certutil-MD5" width="600" height="110">
We will begin by ensuring all of the files provided match the hashes provided. After downloading the archive we may check the MD5 hash of each item using Windows certutil.

<br />

Now that the hashes have been verified and we can assume integrity, we will pull artifacts using numerous forensic analysis toolkits:
<details open><summary><b>Tools</b></summary>
• Autopsy: https://www.autopsy.com/
<br />
• Magnet AXIOM: https://www.magnetforensics.com
<br />
• More To Be Added
    <br />
+ Wireshark & Network Miner (For PCAP Analysis)
</details>

<br />

## Magnet AXIOM (v 4.10.0.23663)
The files contain two recovered sets of machine backups - one titled "Computer1" (E01-E08) and the other "Computer2". To parse the recovered files in Magnet AXIOM a user must first open AXIOM Process and then:
`Create New Case -> Go To Evidence Sources -> Computer -> Windows -> Load Evidence -> Image -> Select Machine1.E01`

<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/76be7711d18ed936754a2e4f216fa74e5d2f978e/imgs/2016-Black-T-Shirt-Forensics-Challenge-%231.png" align="left"
     alt="certutil-MD5" width="320" height="220">

<br />

This ingest was examined with every artifact variant selected which may take somewhat longer than default settings but provides the most comprehensive list. Once Magnet Process has begun we may navigate Magnet Examine and monitor the recovered artifacts. A total of 380,288 artifacts have been gathered for Machine 1 and 12,216 for Machine 2. We will now take a look at some of the interesting information recovered from the artifact extraction process. 

<br /><br /><br />

### Identifying Machines
What can we surmise about the recovered machines themselves from a set of artifacts? Often hardware information, operating system (OS) information, and universally unique identifiers (UUIDs) will reveal information about a machines properties.
<details open><summary><b>IP & Device IDs</b></summary>
    
                            ---------------------------------------------------------------------------
                            | 192.168.0.6 - 192.168.30.1 - 192.168.31.1 |     Registry IPv4 Addr.     |
                            |             DESKTOP-A8BOTBH               |    Comp. Name / Display     |
                            |             WIN-RRKRCRMTOAQ               | Comp. Idnetifier (win logs) |
                            |             DESKTOP-M7P1NB6               | Comp. Idnetifier (win logs) |
                            |              192.168.0.10                 |     Incoming RDP Access     |
                            ---------------------------------------------------------------------------
    
</details>

<details open><summary><b>Volume Information</b></summary>
    
                 -----------------------------------------------------------------------
                 |             Volume Name             |          Volume Type          |
                 |           System Reserved           |           Partition           |
                 |      Seagate Backup Plus Drive      |     Inserted Disk Volume      |
                 | Seagate BUP Slim BK SCSI Disk Device|           USB Device          |
                 |                EXTRAS               |     Inserted Disk Volume      |           ----------------
                 |    Generic Flash Disk USB Device    |          USB Device           |     <     |  Machine 1   |
                 |       Hitachi HTS541660J9SA00       |          USB Device           |           ----------------
                 |      TSSTcorp DVD+-RW SU-208FB      |          USB Device           |
                 |          Integrated Webcam          |          USB Device           |
                 |      CBM Flash Disk USB Device      |          USB Device           |
                 |                OSDisk               |     Inserted Disk Volume      |
                 -----------------------------------------------------------------------
                                                                                                
                               -------------------------------------------------------------------------------------
                               |     Machine 1 -> Microsoft NTFS Paritioned Drives   |          Windows 10         |
                               |       Machine 2 -> EXT-Family Partitioned Drive     |   Ubuntu - Linux web-srv-2  |
                               | VM Within Machine 1 -> EXT-Family Partitioned Drive |             Ubuntu          |
                               -------------------------------------------------------------------------------------
    
</details>
<details open><summary><b>Images</b></summary>
    We can sort the images by last modified/accessed time to retrieve the most likely to be useful images first. Images indicative of operating system information (Default Images) are one method to identify an OS on a given device. Third-party application icons can be used to piece together which applications a user has installed at a given time.

    
                                                           Machine #1
                           ------------------------------------------------------------------------------
                           |           Image Name(s)            |                Summary                |
                           |        Many Starwars Images        | Cached Images of Starward Memorobelia |
                           |      Amazon and Yahoo Images       | Cached Images of Amazon/Yahoo Website |
                           |            Capture.PNG             |        Screenshot of OpenOffice       |
                           ------------------------------------------------------------------------------
    
<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/893bde78fcd62325c217bb3aa35f660f2dde7c93/imgs/BTCFC.gif" align="right"
     alt="BTCTFC" width="200" height="200">
    
                                            Machine #2
            ------------------------------------------------------------------------------
            |           Image Name(s)            |                Summary                |
            |          ubuntu_logo.png           |               Ubuntu Logo             |
            |     BTCTFC.gif & black-t.png       |            Challenge Images           |
            |       Application Icon Set         |         Ubuntu and Gnome Icons        |
            |  3rd Party Application Icon Sets   |   Such as Codeblocks and Thunderbird  |
            ------------------------------------------------------------------------------
    
There is really not much else when it comes to audio or even video for that matter. AXIOM does a great job at carving these files out of cache but these machines in particular do not offer much information in the way of media other than carved out advertisements such as the "Betty Crocker Cookbook".
</details>

</details>
<details open><summary><b>Rebuilt Desktops and Webpages</b></summary>
Magnet AXIOM will go through the work of rebuilding user desktops with the background wallpaper along with desktop files. These images provide a good representation of which applications a user is making the most use of.
    
<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/2ffe3822b5e2c4845ccc402b1ca3c4e9395adc2a/imgs/2016-Black-T-Shirt-Forensics-Challenge-%232.jpg" align="left"
     alt="#2" width="500" height="250">
 
<br /><br />
    
              -----------------------------------------
    <-        |       Mchine #1 - User "tester"       |
              -----------------------------------------
   
<br /><br /><br />
    
<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/e3a3582c66c6a0b1efda1909d977fa3406cdd4d8/imgs/2016-Black-T-Shirt-Forensics-Challenge-%233.png" align="right"
     alt="#3" width="500" height="250">
 
    
<br /><br /><br />
    
    -----------------------------------------
    |       Mchine #1 - User "Carson"       |        ->
    -----------------------------------------
   
<br /><br /><br /><br />

<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/4cc617ea58200fecadaed588cccc4607bf96f15f/imgs/2016-Black-T-Shirt-Forensics-Challenge-%234.png" align="left"
     alt="#4" width="400" height="100">
The same is done for webpage cache. It is worth looking through rebuilt webpages as they often reveal unique login information and graphical proof of user actions. In this case we are able to recover a gmail webpage snippit which displays a user email.

    
<br />
</details>

Now that we have a general understanding of frequently used applications and operating system varience, we can start looking for artifacts pertaining to the "Case".

<br />

### Passwords and Tokens
In the "Passwords and Tokens" results category, four Windows username password hashes have been discovered. Although this tool will not crack the hashes for us, they are common weak NTLM hashes which may be easily cracked manually.
<details open><summary><b>Passwords</b></summary>
    
    ---------------------------------------------------------------------- 
    |    Account    |             NTLM Hash             |    Password    |       ----------------------------------
    |    tester     | F2477A144DFF4F216AB81F2AC3E3207D  |    "monkey"    |   <   |   Hashes were extracted from   |
    | Administrator | 31D6CFE0D16AE931B73C59D7E0C089C0  | Default/Empty  |   <   | "Windows\System32\config\SAM"  |
    |    Carlson    | 32ED87BDB5FDC5E9CBA88547376818D4  |    "123456"    |   <   |       Windows Machine (1)      |
    |   Jonathan    | BECEDB42EC3C5C7F965255338BE4453C  |    "letmein"   |       ----------------------------------
    ----------------------------------------------------------------------
    |   Webmaster   |  NA Taken From Network FTP Logon  |   "Password"   |
    |    Cknight    |  NA Taken From Network FTP Logon  |    "Popcorn"   |
    ----------------------------------------------------------------------
    | evilhenchman  |        N/A (Newtork Hash)         |"MyPassw0rd!@#]"|
    |   henchman    |        N/A (Newtork Hash)         |  "Passw0rd!#"  |
    |    Laslow     |        N/A (Newtork Hash)         |   "FritoLay"   |
    ----------------------------------------------------------------------
                                                                                
The "Administrator" hash is actually just a placeholder hash signifying that a password has not been set yet and the account must be setup. No password will work for this account until it is set by another user with proper permissions.
</details>

<br />
    
### Internet, Email, & Browser Artifacts
AXIOM has recovered 30,000 Web Related artifacts pertaining to everything from search history to Flash Cookies and File Download information.
<details open><summary><b>Autofill, Headers, and Cookies</b></summary>
<img src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/ca21e3ccbb348b3dceda5fbb933f530116994821/imgs/2016-Black-T-Shirt-Forensics-Challenge-%235.png" align="left"
     alt="#4" width="400" height="170">
We will ignore general cookies for the time being, as we will not be able to use them to bypass login due to this challenge being five years old at this point. We can however take a look at Google Chrome, Edge, Firefox, Internet Explorer, and WebKit history along with header information. Google Chrome Autofil and Current Session artifacts provide us assurance of the previously found email.
    
<br /><br />
    
</details>

<details open><summary><b>Downloads</b></summary>

                                                           Machine #1
                           ------------------------------------------------------------------------------
                           |            File Name(s)            |                Source                 |
                           |            vmware_free             |             Edge/IE Cache             |
                           |              firefox               |             Edge/IE Cache             |
                           |          ChromeSetup.exe           |             Firefox Cache             |
                           ------------------------------------------------------------------------------
                               Yes the madlad downloaded Firefox from IE and then Chrome from Firefox
 
</details>
    
<details open><summary><b>Search History / Params</b></summary>
Web related history can point to local device files and may be used to alert us to recently accessed user-created files.
    
                                                               Machine #1
                      -------------------------------------------------------------------------------------------
                      |               Link / Webpage                |                  Source                   |
                      |      C:\Users\Carson\Documents\locked       |         IE Cache (Weekly History)         |
                      |    C:\Users\tester\Documents\HiTek.odp      |         IE Cache (Weekly History)         |
                      |            G:\IP Addresses.txt              |         IE Cache (Weekly History)         |
                      |    Users\tester\Documents\DNS Records.ods   |         IE Cache (Weekly History)         |
                      |    tester\Documents\network-architecture    |         IE Cache (Weekly History)         |
                      |                E:\grays_4.png               |         IE Cache (Weekly History)         |
                      |       E:\Ubuntu 64-bit 15.10.vmwarevm       |         IE Cache (Weekly History)         |
                      |              H:\passwords.txt               |         IE Cache (Weekly History)         |
                      |    C:\Users\Carson\Pictures\Capture.PNG     |         IE Cache (Weekly History)         |
                      |      C:\Users\Carson\Documents\locked       |         IE Cache (Weekly History)         |
                      |     system32\oobe\FirstLogonAnim.html       |         IE Cache (Weekly History)         |
                      |     Dropbox, Box, Ubuntu One, Sky Drive     |          Cloud Services Accessed          |
                      |Flickr, Twitter, Facebook, LinkedIn, Reddit  |      Social Media Services Accessed       |
                      |               Many HTTP Links               |               Chrome Cache                |
                      |   Flapper, WidevineCdm, EV Certs Whitelist  |            Chrome Extentions              |
                      |         mrobinson4614@stevenson.edu         |   FF -  VmWare Parameter (EMail)          |
                      |                 410-940-9782                |   FF -  VmWare Parameter (Phone)          |
                      |             T4WH-M6E3-WRBW-8T9Q             |   FF - VmWare Parameter (Prod Key)        |
                      |                 witchcraft                  |   FF - VmWare Parameter (Username)        |
                      |               Michael Robinaon              |   FF -   VmWare Parameter (Name)          |
                      |            Stevenson University             |   FF - VmWare Parameter (Company Name)    |
                      |     Metasploit Professional Client Links    |   FF -       Virtual Machines             |
                      |    exploit/.../adobe_flash_nellymoser_bof   |   FF -       Virtual Machines             |
                      -------------------------------------------------------------------------------------------
 
</details>

<br />
    
### Documents and Logging
    
<details open><summary><b>Readable Documents</b></summary>
    
                                                           Machine #1
                        ---------------------------------------------------------------------------------------
                        |             Document Name             |                   Summary                   |  
                pdf ->  |            Metasploit Docs            | Many Docs Indicating User Has Installed MSF |
                pdf ->  |            Veracrypt Docs             |       Docs Indicating use of Veracrypt      |
                doc ->  |               notes.doc               |                Word Document                |
                doc ->  |          Next-character.docx          |                Word Document                |
         writer doc ->  |             Projects.odt              |               Writer Document               |
         writer doc ->  |            Evaluations.odt            |               Writer Document               |
         writer doc ->  |              Notes.odt                |               Writer Document               |
         writer doc ->  |           Laser-Widget.odt            |               Writer Document               |
         writer doc ->  |              notes.odt                |               Writer Document               |
         writer doc ->  |              Report.odt               |               Writer Document               |
         writer doc ->  |              Warning.odt              |               Writer Document               |
         writer doc ->  |           B List 2015.odt             |               Writer Document               |
         writer doc ->  |        Happy Birthday Ben.odt         |               Writer Document               |
                        ---------------------------------------------------------------------------------------
 
</details>
    
<details open><summary><b>Logging & Security</b></summary>
    
                                               Machine #1
         ------------------------------------------------------------------------------------
         |             Artifact Name             |                Summary                   |  
         |    VMware Player, Chrome, Firefox     |          Installed Applications          |  
         | VeraCrypt, WinSCP 5.7.6, Adobe Reader |          Installed Applications          |  
         |     Open Office, Realtek Drivers      |          Installed Applications          |
         |          192.168.0.10 - RDP           |  RDP Connection Established, Logged On   |
         | tester, Administrator, Carlson, Guest |        Recovered Account Usernames       |
         |        DefaultAccount, Jonathan       |        Recovered Account Usernames       |
         |   Firefox Setup Stub 42.0.exe->(UPX)  |      Windows Defender Malicious File     | <- sigseq=0x0000055551CE2A24
         |         VMware Player\zip.exe         |      Windows Defender Malicious File     | <- sigseq=0x00000555B74979F0
         |       WinSCP\PuTTY\is-BP5UF.tmp       |      Windows Defender Malicious File     | <- sigseq=0x00000555C1725C4C
         |       WinSCP\PuTTY\puttygen.exe       |      Windows Defender Malicious File     | <- sigseq=0x00000555C1725C4C
         |  IKE and AuthIP IPsec Keying Modules  |         Modified Auth Services           |
         |             Carlson User              |              Remote Logon                |
         |            ANONYMOUS User             |             Network Logon                | <- Anon had access to login to 
         |       Many NT AUTHORITY Logons        |             Service Logon                |          NT AUTHORITY
         ------------------------------------------------------------------------------------
 
</details>
    
<details open><summary><b>Other</b></summary>
    
                                                              Machine #1
                        ---------------------------------------------------------------------------------------
                        |               Artifact Name              |          Summary / Artifact Type         |
                        |               VeraCrypt.exe              |   Antiforensic tool (Seen on Desktop)    |
                        |                  locked                  |              Encrypted File              |
                        |           network-architecture           |              Encrypted File              |
                        |          ev_hashes_whitelist.bin         |              Encrypted File              |
                        | 62A8F87D1165BC1EE9A41CEB9CE5E9D57F37E4CE |              Encrypted File              |
                        |           videoplayback[1].mp4           | Encrypted File (Probably Just Corrupted) |
                        |          Virtual Disk-s001.vmdk          |               Virtual Disk               |
                        |          Virtual Disk-s002.vmdk          |               Virtual Disk               |
                        |          Virtual Disk-s003.vmdk          |               Virtual Disk               |
                        |             Virtual Disk.vdmk            |               Virtual Disk               |
                        ---------------------------------------------------------------------------------------
    
                                                              Machine #2
                        ---------------------------------------------------------------------------------------
                        |               Artifact Name              |         Summary / Artifact Type          |
                        |                 initrd.img               |              Encrypted File              |
                        |                  X3fw.ncf                |              Encrypted File              |
                        |               memtest86+.iso             |                 ISO File                 |
                        ---------------------------------------------------------------------------------------
 
</details>
    
<br />
    
## Autopsy
N/A For Time Being

## All Artifacts
    
                   --------------------------------------------------------------------------------------------
                   |  192.168.0.6 - 192.168.30.1 - 192.168.31.1  |            Registry IPv4 Addr.             |
                   |               DESKTOP-A8BOTBH               |           Comp. Name / Display             |
                   |               WIN-RRKRCRMTOAQ               |        Comp. Idnetifier (win logs)         |
                   |               DESKTOP-M7P1NB6               |        Comp. Idnetifier (win logs)         |
                   |                192.168.0.10                 |            Incoming RDP Access             |
                   |                 Volume Name                 |                Volume Type                 |
                   |              System Reserved                |                 Partition                  |
                   |            Seagate Backup Plus Drive        |           Inserted Disk Volume             |
                   |    Seagate BUP Slim BK SCSI Disk Device     |                 USB Device                 |
                   |                    EXTRAS                   |           Inserted Disk Volume             |           ----------------
                   |        Generic Flash Disk USB Device        |                USB Device                  |     <     |  Machine 1   |
                   |           Hitachi HTS541660J9SA00           |                USB Device                  |           ----------------
                   |          TSSTcorp DVD+-RW SU-208FB          |                USB Device                  |
                   |              Integrated Webcam              |                USB Device                  |
                   |          CBM Flash Disk USB Device          |                USB Device                  |
                   |                    OSDisk                   |            Inserted Disk Volume            |
                   |Machine 1 -> Microsoft NTFS Paritioned Drives|                Windows 10                  |
                   | Machine 2 -> EXT-Family Partitioned Drive   |              Ubuntu - Linux                |
                   |              Many Starwars Images           |  Cached Images of Starward Memorobelia     |
                   |            Amazon and Yahoo Images          |  Cached Images of Amazon/Yahoo Website     |
                   |                 Capture.PNG                 |         Screenshot of OpenOffice           |
                   |                 Image Name(s)               |                 Summary                    |
                   |                ubuntu_logo.png              |                Ubuntu Logo                 |
                   |          BTCTFC.gif & black-t.png           |             Challenge Images               |
                   |            Application Icon Set             |          Ubuntu and Gnome Icons            |
                   |      3rd Party Application Icon Sets        |    Such as Codeblocks and Thunderbird      |
                   |                  tester                     |                   "monkey"                 |
                   |                Administrator                |               Default/Empty                | 
                   |                 Carlson                     |                  "123456"                  | 
                   |                  Jonathan                   |                  "letmein"                 | 
                   |                vmware_free                  |                Edge/IE Cache               |
                   |                  firefox                    |                Edge/IE Cache               |
                   |              ChromeSetup.exe                |                Firefox Cache               |
                   |      C:\Users\Carson\Documents\locked       |          IE Cache (Weekly History)         |
                   |    C:\Users\tester\Documents\HiTek.odp      |          IE Cache (Weekly History)         |
                   |            G:\IP Addresses.txt              |          IE Cache (Weekly History)         |
                   |    Users\tester\Documents\DNS Records.ods   |          IE Cache (Weekly History)         |
                   |    tester\Documents\network-architecture    |          IE Cache (Weekly History)         |
                   |                E:\grays_4.png               |          IE Cache (Weekly History)         |
                   |       E:\Ubuntu 64-bit 15.10.vmwarevm       |          IE Cache (Weekly History)         |
                   |              H:\passwords.txt               |          IE Cache (Weekly History)         |
                   |    C:\Users\Carson\Pictures\Capture.PNG     |          IE Cache (Weekly History)         |
                   |      C:\Users\Carson\Documents\locked       |          IE Cache (Weekly History)         |
                   |     system32\oobe\FirstLogonAnim.html       |          IE Cache (Weekly History)         |
                   |     Dropbox, Box, Ubuntu One, Sky Drive     |           Cloud Services Accessed          |
                   |Flickr, Twitter, Facebook, LinkedIn, Reddit  |       Social Media Services Accessed       |
                   |               Many HTTP Links               |                Chrome Cache                |
                   |   Flapper, WidevineCdm, EV Certs Whitelist  |             Chrome Extentions              |
                   |         mrobinson4614@stevenson.edu         |    FF -  VmWare Parameter (EMail)          |
                   |                 410-940-9782                |    FF -  VmWare Parameter (Phone)          |
                   |             T4WH-M6E3-WRBW-8T9Q             |    FF - VmWare Parameter (Prod Key)        |
                   |                 witchcraft                  |    FF - VmWare Parameter (Username)        |
                   |               Michael Robinaon              |    FF -   VmWare Parameter (Name)          |
                   |            Stevenson University             |    FF - VmWare Parameter (Company Name)    |
                   |     Metasploit Professional Client Links    |    FF -       Virtual Machines             |
                   |    exploit/.../adobe_flash_nellymoser_bof   |    FF -       Virtual Machines             | 
           pdf ->  |               Metasploit Docs               | Many Docs Indicating User Has Installed MSF |
           pdf ->  |               Veracrypt Docs                |       Docs Indicating use of Veracrypt      |
           doc ->  |                  notes.doc                  |                Word Document                |
           doc ->  |             Next-character.docx             |                Word Document                |
    writer doc ->  |                Projects.odt                 |               Writer Document               |
    writer doc ->  |               Evaluations.odt               |               Writer Document               |
    writer doc ->  |                 Notes.odt                   |               Writer Document               |
    writer doc ->  |              Laser-Widget.odt               |               Writer Document               |
    writer doc ->  |                 notes.odt                   |               Writer Document               |
    writer doc ->  |                 Report.odt                  |               Writer Document               |
    writer doc ->  |                 Warning.odt                 |               Writer Document               |
    writer doc ->  |              B List 2015.odt                |               Writer Document               |
    writer doc ->  |           Happy Birthday Ben.odt            |               Writer Document               |
                   |       VMware Player, Chrome, Firefox        |            Installed Applications           |  
                   |    VeraCrypt, WinSCP 5.7.6, Adobe Reader    |            Installed Applications           |  
                   |        Open Office, Realtek Drivers         |            Installed Applications           |
                   |             192.168.0.10 - RDP              |    RDP Connection Established, Logged On    |
                   |    tester, Administrator, Carlson, Guest    |          Recovered Account Usernames        |
                   |           DefaultAccount, Jonathan          |          Recovered Account Usernames        |
                   |      Firefox Setup Stub 42.0.exe->(UPX)     |        Windows Defender Malicious File      | <- sigseq=0x0000055551CE2A24
                   |            VMware Player\zip.exe            |        Windows Defender Malicious File      | <- sigseq=0x00000555B74979F0
                   |          WinSCP\PuTTY\is-BP5UF.tmp          |        Windows Defender Malicious File      | <- sigseq=0x00000555C1725C4C
                   |          WinSCP\PuTTY\puttygen.exe          |        Windows Defender Malicious File      | <- sigseq=0x00000555C1725C4C
                   |     IKE and AuthIP IPsec Keying Modules     |           Modified Auth Services            |
                   |                Carlson User                 |                Remote Logon                 |
                   |               ANONYMOUS User                |               Network Logon                 | <- Anon had access to login to 
                   |          Many NT AUTHORITY Logons           |               Service Logon                 |          NT AUTHORITY
                   |                  VeraCrypt.exe              |     Antiforensic tool (Seen on Desktop)     |
                   |                     locked                  |                Encrypted File               |
                   |              network-architecture           |                Encrypted File               |
                   |             ev_hashes_whitelist.bin         |                Encrypted File               |
                   |    62A8F87D1165BC1EE9A41CEB9CE5E9D57F37E4CE |                Encrypted File               |
                   |              videoplayback[1].mp4           |   Encrypted File (Probably Just Corrupted)  |
                   |             Virtual Disk-s001.vmdk          |                 Virtual Disk                |
                   |             Virtual Disk-s002.vmdk          |                 Virtual Disk                |
                   |             Virtual Disk-s003.vmdk          |                 Virtual Disk                |
                   |                Virtual Disk.vdmk            |                 Virtual Disk                |
                   |                    initrd.img               |                Encrypted File               |
                   |                     X3fw.ncf                |                Encrypted File               |
                   |                  memtest86+.iso             |                   ISO File                  |
                   ---------------------------------------------------------------------------------------------
    
<br />
    
## Manual
Although a good set of artifacts are collated by forensic toolkits, there is just an impossibly large range of what can serve as an artifact. Not all of what we may be looking for is taken into account by the tools and we should always look through the directory structure manually for suspicious and interesting files. Thankfully all of these toolkits provide a dedicated file browser/extractor for us to manually look through.
    
<details open><summary><b>PCAP Analysis</b></summary>
  
For PCAP analysis (we were given a packet capture alongside the disks) we will use Wireshark and Network Miner. Network miner in particular does a great job at automatically carving all downloaded files (over tcp) and providing them to us for analysis as well as providing lists of login attempts. Wireshark provides a more technical and manual interface but can allow for some complex tasks. The provided file - a pcapng file - is not naturally compatible with network miner, so we will convert the file manually before using the tool. To do so we can run the following command: `tcpdump -r input -w output`

<p align="center">
  <img width="500" height="90" src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/0ef94b32b0e3909856f9c3787435957f3b8e9016/imgs/2016-Black-T-Shirt-Forensics-Challenge-%236.png">
</p>
    
<br />

    
    
                                                      PCAP (Network Miner)
                       ----------------------------------------------------------------------------------
                       |             Artifact Name             |        Summary / Artifact Type         |
                       |          192.168.0.8 - Linux          |     FTP Logon - webmaster:password     |
                       |            91.189.91.14/15            |         Ubuntu Distro Download         |
                       |  192.196.0.8/4 - The "HiTeK Folder"   |     Will Have Its Own Section Below    |
                       ----------------------------------------------------------------------------------
 
</details>
    
<details open><summary><b>HiTeK Folder</b></summary>
The recovered TCP files from the 192.168.0.8 IP Address display the companies (HiTeKs) website along with backend files. Within is a zip titled "Secrets.zip" and another titled "BusinessStrategy.zip". These zips are password locked so we cannot see the contents.
In the "Secrets.zip" directory is a file named "Secrets.rtf" and in the "BusinessStrategy.zip" directory is a file named "BusinessStrategy.rtf". To extract these files we must first know the password. Rather than seeking out the password we can just bruteforce it with a wordlist. After cracking the zip password using John The Ripper we sucessfully recover the files. The password for Secrets ended up being "crazylongpassword" and "VeryLongP@ssw0rd" for BusinessStrategy.
    
<p align="center">
  <br />
  <img width="300" height="100" src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/90c546ccc2f6ef5ab93709a1401583872e75a31e/imgs/2016-Black-T-Shirt-Forensics-Challenge-%237.png">
  <img width="380" height="100" src="https://github.com/dragoneyeintel/A-Comparative-Analysis-of-Digital-Forensic-Platform-Artifact-Recovery-Capabilities/blob/90c546ccc2f6ef5ab93709a1401583872e75a31e/imgs/2016-Black-T-Shirt-Forensics-Challenge-%238.png">
  <br />
</p>

Anybody who had access to the HiTeK website was able to download these files and although password protected can crack them as we just saw. In the packet capture the IP Address 192.168.0.4 had downloaded these two files in particular from the server at 192.168.0.8.
</details>
    
<details open><summary><b>Wireshark</b></summary>
To get more information we will open up wireshark and monitor these IP AddressesThe webmaster:password FTP login which we saw earlier is performed by IP 192.168.0.6 afterwhich they had used FTP commands to cd into the www directory and store the two zip files. The user used CHMOD 644 on the files before exiting. The 192.168.0.2 IP was just a dummy machine navigating to the website and checking that the files would download successfully.
</details>
    
## Conclusion
In this scenerio the owners of each machine on the network must be identified and mapped to their IP. It is likely that a competetor organization has planted the files on the webserver but they must have already had some access or an insider as they were working on the local network. This could have been prevented if the password had been set manually and stronger passwords were used across the company.
    
Where digital forensic analysis tools really shine is when carving and fragmented data comes into play. Automated rebuilding of these fragmented memory segments provides us with files and artifacts otherwise unrecoverable by hand. The reason we recieve so many seemingly "useless" artifacts is because well it is hard for a tool to actually know what we as investigators need, so they provide us with all of the information and we can sift through it and find the meaningful artifacts ourselves - and this is the best possible solution. 
