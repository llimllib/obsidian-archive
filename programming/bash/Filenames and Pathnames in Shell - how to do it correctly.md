https://dwheeler.com/essays/filenames-in-shell.html

The summary:

> - Double-quote all variable references and command substitutions unless you are certain they can only contain alphanumeric characters or you have specially prepared things (i.e., use "$variable" instead of $variable). In particular, you should practically always put $@ inside double-quotes; POSIX defines this to be special (it expands into the positional parameters as separate fields even though it is inside double-quotes).
> - Set IFS to just newline and tab, if you can, to reduce the risk of mishandling filenames with spaces. Use newline or tab to separate options stored in a single variable. Set IFS with IFS="$(printf '\n\t')"
> - Prefix all pathname globs so they cannot expand to begin with “-”. In particular, never start a glob with “?” or “*” (such as “*.pdf”); always prepend globs with something (like “./”) that cannot expand to a dash. So never use a pattern like “*.pdf”; use “./*.pdf” instead.
>-  Check if a pathname begins with “-” when accepting pathnames, and then prepend “./” if it does.
> - Be careful about displaying or storing pathnames, since they can include newlines, tabs, terminal control escape sequences, non-UTF-8 characters (or characters not in your locale), and so on. You can strip out control characters and non-UTF-8 characters before display using printf '%s' "$file" | LC_ALL=POSIX tr -d '[:cntrl:]' | iconv -cs -f UTF-8 -t UTF-8
> - Do not depend on always using “--” between options and pathnames as the primary countermeasure against filenames beginning with “-”. You have to do it with every command for this to work, but people will not use it consistently (they never have), and many programs (including echo) do not support “--”. Feel free to use “--” between options and pathnames, but only as an additional optional protective measure.
> - Use a template that is known to work correctly; below are some tested templates.
> - Consider disabling glob matches with leading dashes. As already noted, always prepend globs (e.g., with "./") so you never have a glob with a leading "-". Consider also disabling leading-dash matches, so that if you accidentally forget to do it, the mistake is unlikely to become a security vulnerability. There's no standard way to do that (yet). In bash you can set GLOBIGNORE='-*:.:..' ; notice the -*. The oil shell recently added shopt -u dashglob to disable globs returning leading dashes (this naming is consistent with dotglob in dash; see Oil issue #552 and commit 71124a2b). Then globs will no longer return anything beginning with a bare dash. It is generally wise set up your system to limit the damage of inevitable mistakes.
> - Consider using the unofficial strict mode for shell. This isn't specific to filenames, but it's a good idea in general. The phrase "set -eu" works on all POSIX shells. Use Bash Strict Mode (Unless You Love Debugging) recommends this for bash:
>     #!/bin/bash
>     set -euo pipefail
>     IFS=$'\n\t'
>-  Use a tool like shellcheck to find problems you missed.


It then expands into all of these.
