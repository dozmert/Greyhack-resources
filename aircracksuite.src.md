```
cryptools = include_lib("/lib/crypto.so") // import library containing all the "air" tools.

// airmon
get_shell.launch("/bin/airmon") // list all monitor capable device states
device = user_input("[+]Choose Interface: ") // ask for user to pick device
if not device[0:4] == "wlan" then exit end if // check they at least chose a wireless Interface using slice
print("\n[-]New State...\n")
cryptools.airmon("start", device) // start the device in monitor mode
get_shell.launch("/bin/airmon") // show new state

// iwlist
print("[-]Choose BSSID & ESSID (more PWR% is better)\n")
get_shell.launch("/bin/iwlist", device) // list detected wireless networks
b = user_input("\n[+]BSSID: ") // ask for BSSID
e = user_input("\n[+]ESSID: ") // ask for corrisponding ESSID
acks = user_input("\n[+]ACKs (>7000): ").to_int // ask for ACK count to aim for, and convert to int
print("\n")

if acks < 7000 then acks = 7000 end if // if user enters less than 7000 (the minimum for success) then set it to 7000

// aireplay
cryptools.aireplay(b, e, acks) // run aireplay with the user input from above
print("\n[-]Got Required amount of ACKs...")
print("[-]Waiting for file.cap to be written...\n")
wait(5) // without this aircrack runs immediately and file.cap isnt written yet
print("[-]Cracking...\n")

// aircrack
capfile = current_path + "/file.cap" // set file.cap path
get_shell.launch("/bin/aircrack", capfile) // aircrack the file and display result
print("\n[-]Stopping device monitoring...\n")

// airmon
cryptools.airmon("stop", device) // turn off monitor mode
get_shell.launch("/bin/airmon") // show new state

// clean up
capfile = get_shell.host_computer.File(current_path + "/file.cap") // prep capfile for potential deletion
confirm = user_input("Destroy file.cap (y/N): ")

if confirm == "Y" or confirm == "y" or confirm == "Yes" or confirm == "yes" then capfile.delete end if // delete capfile if user input is yes

print("\n[-]Goodbye...\n")
```