# Bitwarden Login
Script to set the `BW_SESSION` token environment variable and persist with optional encryption to enable re-usability in simultaneous terminal sessions.
## Installation
- Depends on: [bw](https://github.com/bitwarden/cli) (Bitwarden CLI) and [jq](https://stedolan.github.io/jq/download/) (parsing `JSON`)
- Download [bwl](https://raw.githubusercontent.com/tdharris/bitwarden-login/master/bwl)
- Make it executable and reachable. E.g. `chmod +x bwl && sudo cp bwl /usr/local/bin`
## Usage
- To export the `BW_SESSION` environment variable:
    ```bash
    eval $(bwl)
    ```
- Validate:
    ```bash
    echo "${BW_SESSION:-woops}"
    # OR
    printenv | grep 'BW_SESSION'
    ```
## Recommended Configuration
- Create a BitWarden API Key - see [Personal API Key for CLI Authentication](https://bitwarden.com/help/article/personal-api-key/)
- Use `BWL_ENCRYPT_METHOD` to encrypt the persisted session token using either `keybase` or `gpg`
- Use `~/.bwl/config` to persist configuration:
  ```
  BW_CLIENTID=<client_id>
  BW_CLIENTSECRET=<secret>
  BWL_ENCRYPT_METHOD=<gpg|keybase|none>
  GPG_RECIPIENT=<gpg-email>
  ```