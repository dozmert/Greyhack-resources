dmeta  = include_lib("/lib/metaxploit.so")
if not meta then exit("fail 1")
meta.rshell_client("222.203.111.121",1222)
exit("exit 1")