# Actions

A collection of re-usable GitHub actions/workflows.
These are licensed under Apache 2.0 license, so feel free to re-use via your own fork.

# Actions available

## git-config

Configures `git` redirects so that you can use for example `mbed deploy` or other tools that require `git` access to private repositories.


Inputs:
- `github_token` : GitHub access token

Usage example:
```
      - name: Set access token for internal repo access
        uses: PelionIoT/actions/.github/actions/git-config@main
        with:
          github_token: ${{ secrets.ACCESS_TOKEN }}
```
Especially on self-hosted runners it is important to clean out the `.gitconfig` file afterwards. Otherwise access token renewals will not have impact.
```
      - name: Cleanup .gitconfig
        if: always()
        run: rm -f ~/.gitconfig
```

## misspell

Runs the [`misspell`](https://github.com/golangci/misspell) application to spot common spelling mistakes. Exception list (`-i` argument) can be given.
The action assumes the repository has been checked out already.

Inputs:
- `exceptions` - list of words (comma separated, no spaces inbetween) to ignore for spelling mistakes. Typical one would be for example mosquitto (referring to Apache Mosquitto).

Usage example:
```
      - name: Misspell
        uses: PelionIoT/actions/.github/actions/misspell@main
        with:
          exceptions: "mosquitto"
```
