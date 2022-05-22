# Auto updating

Currently packages hosted on github, gitlab or tracked by repology can be auto updated automatically if `TERMUX_PKG_AUTO_UPDATE=true` is set in build.sh

You can use [scripts/bin/check-auto-update](https://github.com/termux/termux-packages/blob/master/scripts/bin/check-auto-update) script to check whether a package can be auto-updated or not.

If automatic updating doesn't work, you may want to override it. See [here](#Overriding).

## Auto update steps refrence

Default update method uses following functions.

Order specifies function sequence. 0 order specifies utility functions.

Suborder specifies a function triggered by the main function. Functions with
different suborders are not executed simultaneously.


| Order | Function Name | Overridable | Description | Parameters |
|------ | ------------- | ----------- | ----------- | ---------- |
| 0.1   | `termux_error_exit` | No | Function to write error message to `stderr` and exit. | Any number of string arguments. You can use heredoc for long messages. |
| 0.2   | `termux_github_api_get_tag` | No | Query GitHub API for: <br><br> &bull; `latest-release-tag`: useful for projects using github's release mechanism. <br><br> &bull; `newest-tag`(sorted by commit date): useful for projects having tags but no releases. | &bull; PKG_SRCURL - Source url of package. <br><br> &bull; TAG_TYPE - Optional. Type of tag to query. It is one of the queries mentioned in description. If not given it is decided on the basis of PKG_SRCURL. For urls ending in `.git` `newest-tag` is queried, otherwise `latest-release-tag`.|
| 0.3   | `termux_gitlab_api_get_tag` | No | *same as above, but for gitlab* | *same as above, except for optional 3rd argument:* <br> &bull; API_HOST - Host for gitlab api. Default `gitlab.com`. |
| 0.4   | `termux_repology_api_get_latest_version` | No | Query repology api for latest version. | &bull; PKG_NAME - Name of the package to query for. |
| 1     | `termux_pkg_auto_update` | Yes | By default, decide which method (gitlab, github or repology) to use for update, but can be overrided to use custom method. | *None* |
| 2.1     | `termux_github_auto_update` | No | Default update method for packages hosted on github.com. It decides which type of tag to fetch based on `TERMUX_PKG_SRCURL`. | *None* |
| 2.2     | `termux_gitlab_auto_update` | No | Default update method for packages hosted on gitlab.com (or host specified by `TERMUX_GITLAB_API_HOST`). It decides which type of tag to fetch based on `TERMUX_PKG_SRCURL`. | *None* |
| 3       | `termux_pkg_upgrade_version` | No | Write the latest version and updated checksum, check whether updated package builds properly and then push changes to repo. | &bull; LATEST_VERSION - version to write to build.sh. <br><br> &bull; --skip-version-check - Optional flag. Do not check whether given LATEST_VERSION is greater than current TERMUX_PKG_VERSION. |
| 3.1     | `termux_pkg_is_update_needed` | No | Check whether LATEST_VERSION is greater than TERMUX_PKG_VERSION or not. <br> Called if `--skip-version-check` was not passed to `termux_pkg_upgrade_version`. <br><br> **NOTE:** You should not call it manually otherwise if `TERMUX_PKG_UPDATE_VERSION_REGEXP` is used, it won't compare versions extracted from it. Version is extracted by `termux_pkg_upgrade_version`. | *Not for public use.* |

## Overriding

Where automatic update dosen't work, you may override `termux_pkg_auto_update()` function to write your own steps.

For example see [neovim-nightly's build.sh](https://github.com/termux/termux-packages/blob/3c617f6222405cc51935bb13d557eb0b7b6fe95f/packages/neovim-nightly/build.sh#L27).

- All functions marked as utility here, are available within `termux_pkg_auto_update()` or functions spawned by it.
- You should call `termux_pkg_upgrade_version` with LATEST_VERSION to write changes to build.sh

---
**Warning**

Bash *fail-fast* (i.e `set -euo pipefail`) is set, so consider it during error handling.

*Read more about bash fail-fast [here](https://dougrichardson.us/notes/fail-fast-bash-scripting.html).*

For example:

Following code won't work as expected:
```bash
local curl_response
curl_response=$(curl --silent "https://example.com" --write-out '|%{http_code}')

# XXXX: following code won't execute if curl fails as script will exit immediately there.

local http_code="${curl_response##*|}"
if [[ "${http_code}" != "200" ]]; then
	echo "Error: failed to get latest version."
	exit 1
fi
```
Instead use something like:
```bash
local curl_response
curl_response=$(
	curl --silent "https://example.com" --write-out '|%{http_code}'
) || {
        # This will run as expected.
	local http_code="${curl_response##*|}"
	if [[ "${http_code}" != "200" ]]; then
		echo "Error: failed to get latest version"
		exit 1
	fi
}
```
---