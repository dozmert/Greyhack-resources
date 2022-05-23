```
//// Variables
currentpath = current_path+"/"
routerapp = "scanrouter2"
dirRouter = current_path+"router/"
targetTypeReg=0
//// Code start
print("Bulldozer v1.2")
//Target Address
print("Target Address? xxx.xxx.xxx.xxx")
//targetAddress = (user_input("input: "))
targetAddress = "192.168.0.1"

//Target type
print("Target type? 1.Router 2.X 3.Y")
while targetTypeReg==0
	targetType=0
	targetType = (user_input("input: "))
	targetType = targetType.to_int
	if targetType == 1 then
  		print ("Pass")
  		targetTypeReg=1
 	else
  		print ("Fail")
  		continue
 	end if
end while
//Router
if targetType == 1 then
	print("Router payload...")
	//routerScan = get_shell.launch(currentpath+routerapp, targetAddress)
	//print(targetAddress.kernel_version)
	router = get_router(targetAddress)
	if router == null then
		print("scanrouter: ip address not found")
	else 
		routerVersion = router.kernel_version
		print(routerVersion)
		routerPayload = dirRouter+routerVersion+"/"
		for payload in routerPayload////////////////stuck here
			print("1")
		end for
		x = routerPayload.get_content
		print(x)
	end if
end if
targetAddress = (user_input("End?"))
print("Script completed.")
////Code end
```