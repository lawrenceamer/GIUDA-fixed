# GIUDA
GET a TGS on behalf of another user without password

Scenario: you are Local Administrator and there is a logged User you want to Impersonate!

Chain: SeTcbPrivilege allows you to read LSA storage, extract the SESSION KEY from TGT, and forge a request asking for a TGS; You must use LUID instead of Username.

Goal: From Local Admin to Domain Admin with Kerberos TGS

Required: Local Administrator and a Domain Admin Logged (or Disconnected). In this guide the Domain Admin User is CALIPENDULA\fagiolo

1. ask to GIUDA for a shell as SYSTEM
2. GIUDA -runaslsass            or
3. GIUDA -runaspid:PID          (a NT AUTHORITY\SYSTEM's PID, enumerate by yourself) you need a PID running with SeTcpPrivilege, search well and try also WINLOGON's PID!
![image](https://github.com/foxlox/GIUDA/assets/28823598/a04903ea-de62-4f57-951f-655c45ab26e4)


4. ask to GIUDA to show ALL Logged User's LUID
5. GIUDA -askluids

![image](https://github.com/foxlox/GIUDA/assets/28823598/b39e3839-b499-4bbc-b011-ab638ddc2874)


6. take the LUID that you want to impersonate and ask GIUDA to get the msdsspn that you want
![image](https://github.com/foxlox/GIUDA/assets/28823598/d1ce1a96-a6fc-4588-ade8-1212d7140cfa)

7. use PSSession to log on the Domain Controller
![image](https://github.com/foxlox/GIUDA/assets/28823598/5bef5372-f49c-4591-886e-7712158538c6)


# Optional
Optionally you can ask to SAVE the TGS and pass it next or on another Machine (also on Linux, but only if USER doesn't require PREAUTH, because you have only a TGS without TGT)

8. ask TGS with -save option. GIUDA'll save a file named TICKET.KIRBI so you can copy it
![image](https://github.com/foxlox/GIUDA/assets/28823598/5e7bc1c2-5b8c-4ed1-881e-4d62ed2eea08)

# Compiling 
for compiling the project you need lazarus-ide and you need to download offline copy of https://sourceforge.net/projects/jedi-apilib/
- install lazarus on your system.
- extract the content of jedi zip files into local folder on your system for example c:\TMP\jwa\..
- go to project => options => paths and make sure to include the path of winapi units into the project, you can see the picture below fore reference.
![image](https://github.com/lawrenceamer/GIUDA-fixed/assets/10256911/2e0fffc9-7f5a-4a87-bf6e-d62536d8dbcc)
- hit build and get it ready.

# Thanks
A very big thanks to Erwan22, he does a very powerful set of Pascal Units for AD. Thx Erwan22, you're really great!
