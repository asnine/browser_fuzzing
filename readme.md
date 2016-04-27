##How to using it
---
###Fuzzing
1.run `open_console_in_this_dir.bat`<br/><br/>
![step_1](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_1.jpg)<br/><br/>
2.run `web_server.py` in this new console window<br/><br/>
![step_2](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_2.jpg)<br/><br/>
3.using your browser which you want to fuzzing to open `http://127.0.0.1/vector`<br/><br/>
![step_3](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_3.jpg)<br/><br/>
4.using `get_poc.py` dump crash poc when browser has been crash<br/><br/>
![step_4_1](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_4_1.jpg)<br/><br/>
![step_4_2](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_4_2.jpg)<br/><br/>
![step_4_3](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_4_3.jpg)<br/><br/>
5.repeat crash in browser<br/><br/>
![step_5_1](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_5_1.jpg)<br/><br/>
![step_5_2](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_5_2.jpg)<br/><br/>
<br/>

###Valid PoC File
1.run `valid_server.py`<br/><br/>
![step_6](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_6.png)<br/><br/>
2.run `valid_poc.py`<br/><br/>
![step_7](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/step_7.png)<br/><br/>
WARNING! Sometime Browser Will Follwing Down in DeadLoop .Just Using `taskmgr.exe` to Kill it .`valid_poc.py` Will Recall Browser EXE<br/>
TIPS :If you get a Exploit File ,Congratulation you !This file will be save to dir **exploit**
<br/>

###How to using valid_poc.py
`valid_poc.py` will help you dig valueable PoC in all crash files,using :<br/><br/>
**valid_poc.py** %poc_index%  --  test a poc<br/>
**valid_poc.py** %poc_index% debug  --  test a poc and output more detail<br/><br/>
if you want to get more detail in analays crash files information ,plaese start `valid_poc_debug.py`.you can see that instruction where will crash<br/><br/>
![step_8](https://raw.githubusercontent.com/lcatro/browser_fuzzing/master/pic/add_show_debug_detail.png)

###About valid_server.py
You can not execute a JavaScript or VBScript in Internet Explorer still load in file:// .So I make this WEB Server to resolve this probleam ,this is Using :
**valid_server.py**  --  run server(it will load crash file from path \poc)<br/>
**valid_server.py** debug  --  run server(it will load crash file from path \exploit)<br/>
if you want to debug a exploit file ,using `valid_server.py debug` and `valid_poc.py %CrashFileIndex% debug` .`valid_poc.py` include a small debugger (support:-r %regesit% (look regesit) ;-a %address% (look memory address) ;-u %address% (get instruction) ;-quit (will exit)).<br/><br/>
if you want to all automation ,plaese using `valid_poc_debug.py`

###Other Envirment Setting
1.Set IE Single Process -> `set_ie_single_process.reg`<br/><br/>
2.Set disable system crash tips window -> `clear_system_debug_tips_window.reg`<br/><br/>

---
so ,this is a full step to collect a crash PoC ,but i write a auto fuzzing script -- process_monitor.py .You just need set some argerment about target fuzzing browser path .etc .Good luck ! ..
<br/>
TIPS 1:If you have not install pydasm ,download link :https://github.com/reider-roque/pydbg-pydasm-paimei<br/>
TIPS 2:You need manual setting some setting about Internet Explorer .I packet these import setting to Regesit File ,care
`clear_system_debug_tips_window.reg`**(You Need Manual Setting Regesit Item Value to the diable_system_debug_tips_window.exe's full path )** and `set_ie_single_process.reg`<br/>
TIPS 3:Add `valid_poc.py` and `valid_server.py` .First ,start `valid_server.py` to run a WEB server for valid Fuzzing PoC is or not a valid Vuln ;and than ,run `valid_poc.py` call Browser getting this PoC to process and `valid_poc.py` will analysis crash file ,if this is a Vuln Crash File,it will save this PoC to dir **exploit**<br/>
TIPS 4:May you need to setting what browser you want to test path in `process_monitor.py` and `valid_poc.py`<br/>
