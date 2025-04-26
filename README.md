# Blue Team Field Notes

A dump of (hopefully) useful things for all things blue.

## Environment Configuration

### Shell Timestamps

Timestamps are important and UTC is the gold standard for forensic investigations. Here's how to set your terminal up so that you always have the current UTC time at a glance.

#### Bash

```
# Edit .bashrc file
$ vim ~/.bashrc

# [date time (UTC)] 
# E.g., 2024-06-12 13:37:51 UTC
PS1='\[\033[00;35m\][`date -u +"%Y-%m-%d %T %Z"]` ${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Source the amended file to ensure the shell updates
$ source ~/.bashrc
```

![[images/Pasted image 20241222160516.png]]

Other: [How To Customize and Colorize your Bash Prompt - HowToGeek](https://www.howtogeek.com/307701/how-to-customize-and-colorize-your-bash-prompt/)

#### PowerShell

```
# Create a PowerShell profile
PS > New-Item $Profile -ItemType file –Force

# Edit and add line
function prompt{ "[$(Get-Date)]" +" | PS "+ "$(Get-Location) > "}

# Change execution policy to ensure the prompt updates
PS > Set-ExecutionPolicy RemoteSigned
```

![[images/Pasted image 20241222161713.png]]

#### CMD

```
>setx prompt $C$D$S$T$H$H$H$SUTC$F$S$P$S$G$S

:: Reference: https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/prompt
:: $H are to remove the additional microsecond timestamp from $T
```

![[images/Pasted image 20250223162244.png]]



## N






## Hashes

The hash of a malicious file is a vital indicator of compromise that can be acquired during the intelligence development stage of response. This can then be used to search across the environment to identify additional hosts that may be impacted by the same malware as well as to profile the threat actor.

Hashes can also be searched across open source resources, such as [VirusTotal](https://www.virustotal.com/), to see if this has been identified previously. However, it is best **NOT to upload** or share the raw binary publicly until you have remediated the campaign in your own environment. Threat actors frequently watch to see if they have been identified; if they see their malware on public sources, they may ramp up their activities within environments which they have compromised (see: **Early Remediation**).

### Getting Hashes

#### PowerShell / Command Prompt (Windows)

```
# Replace SHA256 with MD5/SHA1, etc. as needed
PS > Get-FileHash -Algorithm SHA256 \path\to\file
```

```
> sha256sum.exe \path\to\file
```

#### Bash (Linux)

```
$ sha256sum /path/to/file
```




# Splunk

It is best practice to use [epoch time](https://www.epochconverter.com/) when sharing queries so that the time period and data results remain should the search be reviewed in future.

```
earliest=1735689600 latest=1738371600
```

If relative time has been used, e.g., `earliest=-7d@d latest=now`, the epoch time is populated in the URL and can be extracted as follows:

```

```