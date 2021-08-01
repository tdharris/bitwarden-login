# Bitwarden Login
Script to set the `BW_SESSION` token environment variable and persist with optional encryption to enable re-usability in other terminal sessions.
## Installation
- Depends on: [bw](https://github.com/bitwarden/cli) (Bitwarden CLI) and [jq](https://stedolan.github.io/jq/download/) (parsing `JSON`)
- Download [bwl](https://raw.githubusercontent.com/tdharris/bitwarden-login/master/bwl)
- Make it executable and reachable. E.g. `chmod +x bwl && sudo cp bwl /usr/local/bin`
## Usage
- To export the `BW_SESSION` environment variable:
    ```shell
    eval $(bwl)
    ```
- Quick demo:
    ```shell
    # Show that the BW_SESSION environment variable is not loaded.
    $ echo "${BW_SESSION:-nope}"
    nope

    # Show that bw is unauthenticated
    $ bw status | jq '.status'
    "unauthenticated"

    # Execute and evaluate bwl
    $ eval $(bwl)
    ? Master password: [hidden]

    # Show that the BW_SESSION environment variable is loaded.
    $ echo "${BW_SESSION:-nope}"
    [hidden]

    # Show that bw is unlocked
    $ bw status | jq '.status'
    "unlocked"
    ```
## Recommended Configuration
- Create a BitWarden API Key to simplify login - see [Personal API Key for CLI Authentication](https://bitwarden.com/help/article/personal-api-key/). *Note: This approach still requires the vault to be `unlocked`, which prompts for the `Master password` if there is no existing session file.*
- Use `BWL_ENCRYPT_METHOD` to encrypt the persisted session token using either `keybase` or `gpg`.
- Use `~/.bwl/config` to persist the configuration:
  ```
  BW_CLIENTID=<client_id>
  BW_CLIENTSECRET=<secret>
  BWL_ENCRYPT_METHOD=<gpg|keybase|none>
  GPG_RECIPIENT=<gpg-email>
  ```
