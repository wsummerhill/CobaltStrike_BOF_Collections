# CobaltStrike BOF Collections
Useful Cobalt Strike BOFs found or used during red teaming and penetration testing engagements

### Executing .NET Assemblies

- [**InlineExecute-Assembly**](https://github.com/anthemtotheego/InlineExecute-Assembly)<br />
Perform .NET assembly execution of any .NET executable without any prior modifications required<br />
The BOF also supports several flags to disabling AMSI via in memory patching, disabling and restoring ETW via in memory patching, or customization of the CLR App Domain name to be created<br />
```inlineExecute-Assembly --dotnetassembly /home/Seatbelt.exe --assemblyargs AntiVirus AppLocker --etw --amsi --mailslot totallyLegitMailslot```

- [**inject-assembly**](https://github.com/kyleavery/inject-assembly)<br />
Another alternative .NET executable loader to inject an assembly into a running process<br />
```inject-assembly 0 /home/Rubeus.exe [args...]```

- []()

- []()

- []()

- [**Situational Awareness BOF**](https://github.com/trustedsec/CS-Situational-Awareness-BOF)<br />
BOF that provides host enumeration and awarness commands which are more opsec friendly<br />
Example commands include:
```
arp --> List arp tables
ipconfig --> Run ipconfig
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



- []()

- []()
