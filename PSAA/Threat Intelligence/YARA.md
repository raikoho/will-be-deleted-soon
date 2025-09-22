[https://yara.readthedocs.io/](https://yara.readthedocs.io/)
https://github.com/Neo23x0/signature-base

```
rule TextExample
{
    strings:
        $text_string = "foobar"

    condition:
        $text_string
}
// if text_string matches in program - it will show output
```

------------

u can use `strings program.exe`
grab some strings
and create the yara rule with this.

use also "and" "and not" "or"
## Example (Mimikatz)

![[Pasted image 20250129171812.png]]

"`Pe_signature` at 0" means "MZ" will be show at the 0 string (in the start position).