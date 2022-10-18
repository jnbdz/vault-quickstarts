# SSH | Secrets Engines | Vault
This Vault engine provides auth and authz for access to machines via the SSH protocol.

Provides serveral ways to issue SSH credentials.

Here are the modes: 
## Signed SSH Certificates
- Simplest
- Most powerful (setup complexity & platform agnostic)
- Leverages Vault's powerful CA capabilities and funtions in OpenSSH

> The term **client** -> person or machine performing the *SSH operation*.
> The term **host** -> target machine.

**Doc:** 
```bash
vault path-help
```



## One-time SSH Passwords
This sercrets engine allows a Vault server to issue a OTP every time a client wants to SSH into a remote host using a helper command on the remote host to perform verification.

Drawbacks:
> The remote host's connection to vault if compromised an attacker could modify the Vault server return message to successful request.
> You can add security with a TLS connection.
> There might be improvements in the future comign from the Vault team.



## Dynamic SSH Keys<sup>DEPRECATED</sup>

## Resources
- [Dynamic SSH Keys | vaultproject](https://www.vaultproject.io/docs/secrets/ssh/dynamic-ssh-keys)
### Videos
 - [Leveraging Signed SSH for Remote Access with Vault | YouTube](https://www.youtube.com/watch?v=P93f7eQdecg)
