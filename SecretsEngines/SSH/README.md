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

> The first step is to configure the Vault SSH secrets engine before a client can request their SSH key.
> Normally a security deals with this.
> It is possible to automate with Ansible.

### Configuration
1. Set env variables: 
    ```bash
    export VAULT_ADDR='http://127.0.0.1:8200'
    export VAULT_TOKEN=""
    ```
> If you are using a container you need to add inside the container: `podman exec -it <container name> sh`

> It is the solution to this error: 
> `Error enabling: Post "https://127.0.0.1:8200/v1/sys/mounts/ssh-client-signer": http: server gave HTTP response to HTTPS client`

2. Mount the secret engine: 
	```bash
	$ vault secrets enable -path=ssh-client-signer ssh
	```
3. Generate Keypair: 
    ```bash
    vault write ssh-client-signer/config/ca generate_signing_key=true
    ```

4. ...
    ```bash
    curl -o /etc/ssh/trusted-user-ca-keys.pem http://127.0.0.1:8200/v1/ssh-client-signer/public_key
    ```
    ```bash
    vault read -field=public_key ssh-client-signer/config/ca > /etc/ssh/trusted-user-ca-keys.pem
    ```
    ```bash
    # /etc/ssh/sshd_config
    # ...
    TrustedUserCAKeys /etc/ssh/trusted-user-ca-keys.pem
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
