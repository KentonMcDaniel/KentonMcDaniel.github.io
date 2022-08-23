My results for the Vulnerable service review.

Code to review can be found at: https://github.com/KentonMcDaniel/VulnerableService

My answers:

Encryption.cs:

(https://github.com/KentonMcDaniel/VulnerableService/blob/main/Encryption.cs)


There are hard coded encryption keys and IVs:

Because the key is hard coded, this means that all data would be compromised once this key and IV are discovered.

Using AES128 which is completely acceptable.

The encryption algorithm never actually returns the ciphertext as encrypted data:

The DPAPI is being used with local system permissions and no entropy:
This means that all secrets being protected with the DPAPI are available to all users on the system and are trivial to recover.

TaskRunner.cs:
(https://github.com/KentonMcDaniel/VulnerableService/blob/main/TaskRunner.cs)

Overall observations about this service:

This is running as a Windows Service which means it is likely running with elevated permissions (likely SYSTEM permissions). Any vulnerability here is likely a privilege escalation.
RunBackup Method:
 

The method is checking for something in a non-standard windows folder: “C:\DevTools\”. Because this is a non-standard folder, the permissions of this folder should automatically be under scrutiny. This particular method is checking for a text file, and if the text file does not exist it is calling into C:\DevTools\Backup.exe without verifying the permissions or integrity of that file. This is likely a privilege escalation due to no integrity validation.

RunHelperFunctions Method:
 

This method is checking to see if there is a text file on disk at the same C:\DevTools\ location. If the text file does not exist, it is then running the default entry point of the .dll named Helper.dll. This is a privilege escalation vector.

RunRegistryCommand Method:

We are looking at a non-standard Registry Key. This registry key being checked could likely be overwritten with our payload that would grant us a privilege escalation.
