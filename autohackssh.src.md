//Imports
metaLib = include_lib("/lib/metaxploit.so")
if not metaLib then
    metaLib = include_lib(current_path + "/metaxploit.so")
end if
if not metaLib then exit("Error: Can't find metaxploit.so library in the /lib path or the current folder")

cryptLib = include_lib("/lib/crypto.so")
if not cryptLib then
    cryptLib = include_lib(current_path + "/crypto.so")
end if
if not cryptLib then exit("Error: Can't find crypto.so library in the /lib path or the current folder")

//Variables

//publicIP = user_input("Public IP: ")
targetPublic1 = "193.43.29.27" //debugging
//privateIP = user_input("Private IP: ")
//portAddress = user_input("Port Number: ")
localPC = get_shell.host_computer
currentPath = current_path //Get path of current binary
outputFolder0 = "autohackSSH-Output" //Output folder
outputFolder1 = currentPath+"/"+outputFolder0 
//Create OutputDIR
localPC.create_folder(currentPath,outputFolder0)
print(localPC.touch(outputFolder1, targetPublic1 + ".txt"))
//empFile = current_path/publicIP + ".txt"
//nmapScan = get_shell.launch(current_path + "/tools/nmap", publicIP)
//tempFile.set_content nmapScan
