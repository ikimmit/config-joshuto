# Joshuto Config

__My config files for the excellent joshuto file explorer__


### CD on quit

This allows me to automatically cd to joshuto's cwd upon quitting.

It requires:
* a custom keymap (check `keymap.toml` file)
* a bash function to wrap the joshuto invocation

Here is the bash function (picked from some forum):

```
function joshuto() {
	ID="$$"
	mkdir -p /tmp/$USER
	OUTPUT_FILE="/tmp/$USER/joshuto-cwd-$ID"
	env joshuto --output-file "$OUTPUT_FILE" $@
	exit_code=$?

	case "$exit_code" in
		# regular exit
		0)
			;;
		# output contains current directory
		101)
			JOSHUTO_CWD=$(cat "$OUTPUT_FILE")
			cd "$JOSHUTO_CWD"
			;;
		# output selected files
		102)
			;;
		*)
			echo "Exit code: $exit_code"
			;;
	esac
}
```
