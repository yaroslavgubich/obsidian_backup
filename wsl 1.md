
#paste #clipboard #wsl1


It hung because Bash never got a _properly-closed_ quote, so it just kept waiting for the rest of the command.  
Here’s a rock-solid call that works in WSL 1 (no alias yet, just run it as-is):

```bash
/mnt/c/Windows/System32/WindowsPowerShell/v1.0/powershell.exe \
  -NoLogo -NoProfile -Command 'Get-Clipboard -Raw'
```

## Things to notice

|What|Why it matters|
|---|---|
|**Back-slashes ( \ )**|Just to split the long line for readability – they’re optional.|
|**Single quotes around the PS script**|Bash treats everything between the single quotes literally, so the pipe symbol and spaces go to PowerShell intact and the quote is _properly terminated_.|
|**`-Raw`**|Forces PowerShell to dump clipboard text exactly as-is (no line-by-line buffering).|
|**`-NoLogo -NoProfile`**|Faster; prevents PS from loading your Windows profile every call.|

## Quick test

1. Copy the word **hello** in Windows.
    
2. Run the command above in WSL → you should see:
    

```
hello
```

## If that succeeds, add the alias

Append to the end of **`~/.bashrc`**:

```bash
alias paste='/mnt/c/Windows/System32/WindowsPowerShell/v1.0/powershell.exe -NoLogo -NoProfile -Command '\''Get-Clipboard -Raw'\'''
```

_(Notice the extra `'\''` sequence – that’s how you embed single quotes inside single-quoted Bash strings.)_

Then reload and try it:

```bash
source ~/.bashrc
paste
```

## Still nothing?

If you still get no output, the culprit is usually **RDP clipboard redirection**:

1. On the _client_ machine, check **Remote Desktop Connection ▸ Show options ▸ Local resources ▸ Clipboard** (must be ticked).
    
2. On the _server_ (WS 2019) run `gpedit.msc` → **Computer Configuration ▸ Admin Templates ▸ Windows Components ▸ Remote Desktop Services ▸ Remote Desktop Session Host ▸ Device and Resource Redirection ▸ Do not allow Clipboard redirection**. Make sure it’s **Not configured** or **Disabled**.
    
3. Log off / back on to the RDP session.
    

After clipboard redirection works on Windows, the `paste` alias inside WSL will work as well.