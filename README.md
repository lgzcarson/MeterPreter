[![Version](https://img.shields.io/badge/Meterpreter_Paranoid_Mode-1.4-brightgreen.svg?maxAge=259200)]()
[![Stage](https://img.shields.io/badge/Release-Stable-brightgreen.svg)]()
[![Build](https://img.shields.io/badge/Supported_OS-kali,Mint,Ubuntu-blue.svg)]()



## Meterpreter_Paranoid_Mode v1.4 - SSL/TLS connections
    Version release: v1.4 (Stable)
    Author: pedro ubuntu [ r00t-3xp10it ]
    Distros Supported : Linux Kali, Mint, Ubuntu
    Suspicious-Shell-Activity (SSA) RedTeam develop @2017

<br /><br />

## Description:
     Meterpreter_Paranoid_Mode.sh allows users to secure your staged/stageless
     connection for Meterpreter by having it check the certificate of the
     handler it is connecting to.

     We start by generating a certificate in PEM format, once the certs have
     been created we can create a HTTP or HTTPS or EXE payload for it and give
     it the path of PEM format certificate to be used to validate the connection.

     To have the connection validated we need to tell the payload what certificate
     the handler will be using by setting the path to the PEM certificate in the
     HANDLERSSLCERT option then we enable the checking of this certificate by
     setting stagerverifysslcert to true.

     Once that payload is created we need to create a handler to receive the
     connection and again we use the PEM certificate so the handler can use the
     SHA1 hash for validation. Just like with the Payload we set the parameters
     HANDLERSSLCERT with the path to the PEM file and stagerverifysslcert to true.

     We can see the stage doing the validation when we recibe a session back ..
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/cNoQaV.png)

 
## Exploitation:
    Meterpreter_Paranoid_Mode tool starts posgresql service, builds the PEM certificate,
    builds payload (staged OR stageless), starts the comrespondent handler associated to
    the PEM certificate created (manual) OR impersonated (msf auxliary module) runs msf
    post-exploitation modules at session creation, deliver agents (staged or stageless)
    using hta attack vector (apache2 + hta + agent) if configurated in the settings file.

## Payloads available:
    Staged (payload.bat|ps1|txt|exe):
    windows/meterpreter/reverse_winhttps
    windows/meterpreter/reverse_https
    windows/x64/meterpreter/reverse_https

    Stageless (binary.exe):
    windows/meterpreter_reverse_https
    windows/x64/meterpreter_reverse_https

<br /><br />

## Dependencies/Limitations:
    xterm, zenity, metasploit, postgresql


    WARNING: This tool will NOT evade AV detection, its made to prevent the data
    beeing transmited from client (payload) to server beeing captured (Eavesdropping)

    WARNING: If you decided to use a 64bit payload, then edit settings file and change
    'MSF_ENCODER=x86/shikata_ga_nai' to one payload arch compatible encoder(64bit)

    WARNING: Only in 'staged' builds, Users are allowed to chose the extension (bat|ps1|txt|exe)

<br /><br />

## Config Settings file (warning: case sensitive)
msf postgresql database connection check? (msfdb reinit)
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/UHeSaL.png)
Default payload extension (output) to use in staged builds
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/TJ3key.png)
Input agent (output) name manually
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/VsKyIE.png)
Metasploit encoder to use in obfuscating payload sourcecode
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/McAQNP.png)
This tool will also encode the 'stage' beeing send (sending stage to 192.168.1.69:666 ..)
<br />
using the encoder + unicode_encoder sellected on settings file (default: x86/shikata_ga_nai)
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/m1G2TR.png)
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/IpyB2u.png)
<br />
HTA attack vector (deliver agent in local lan using apache2)
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/nqjahX.png)
<br />
Default msf post module to run at session creation
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/gvpBiY.png)

<br /><br />

## Download/Install/Config:
    1?? - Download framework from github
         git clone https://github.com/r00t-3xp10it/Meterpreter_Paranoid_Mode-SSL.git

    2?? - Set files execution permitions
         cd Meterpreter_Paranoid_Mode-SSL
         sudo chmod +x *.sh

    3?? - Config tool settings
         nano settings

    4?? - Run main tool
         sudo ./Meterpreter_Paranoid_Mode.sh

<br /><br />

## Tool screenshots:
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/EtznB0.png)
![Meterpreter_Paranoid_Mode v1.4](http://i.cubeupload.com/Xn9sMT.png)

<br />

## Video tutorials:
MPM [ Stageless payload - exe ]: https://www.youtube.com/watch?v=czbpD_4Mcdw

MPM [ Staged payload - bat ]: https://www.youtube.com/watch?v=Z51jBiFnPGE

MPM [ Stageless payload -exe - set encoder and post-module ]: https://www.youtube.com/watch?v=EBZq-JpGQMM

MPM [ Staged payload - ps1 - HTA attack vector ]: https://www.youtube.com/watch?v=JuoczGI4B3E

<br />

### Special thanks (POCs):
**@hdmoore** | **@OJ** | **@darkoperator** | **Milton@barra(SSA)**

http://buffered.io/posts/staged-vs-stageless-handlers/

https://github.com/rapid7/metasploit-framework/wiki/Meterpreter-Paranoid-Mode

https://www.darkoperator.com/blog/2015/6/14/tip-meterpreter-ssl-certificate-validation

**Suspicious-Shell-Activity (SSA) RedTeam develop @2017**
