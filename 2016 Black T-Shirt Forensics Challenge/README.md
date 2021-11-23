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
    
</details>

### Summary
Table Here

## Autopsy
NULL
