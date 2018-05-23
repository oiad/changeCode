# changeCode
Set custom Safe/Lockbox/Door codes when placed and allow changing of codes

* Discussion URL: https://epochmod.com/forum/topic/45116-change-code-change-lockbox-safe-and-door-codes/

* Tested as working on a blank Epoch 1.0.6.2 server
* This will allow players to set the code on placement/upgrade of doors, lockboxes and safes as well as changing them after they are placed.

# REPORTING ERRORS/PROBLEMS

1. Please, if you report issues can you please attach (on pastebin or similar) your CLIENT rpt log file as this helps find out the errors very quickly. To find this logfile:

	```sqf
	C:\users\<YOUR WINDOWS USERNAME>\AppData\Local\Arma 2 OA\ArmA2OA.RPT
	```

# Install:

* This install basically assumes you have NO custom variables.sqf or compiles.sqf or fn_selfActions.sqf, I would recommend diffmerging where possible.

**[>> Download <<](https://github.com/oiad/buryBodies/archive/master.zip)**

# Mission folder install:

1. In mission\init.sqf find: <code>call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\variables.sqf";</code> and add directly below:

	```sqf
	call compile preprocessFileLineNumbers "dayz_code\init\variables.sqf";
	```

2. In mission\init.sqf find: <code>call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\compiles.sqf";</code> and add directly below:

	```sqf
	call compile preprocessFileLineNumbers "dayz_code\init\compiles.sqf";
	```

3. Copy the <code>dayz_code</code> and <code>scripts</code> folder from the repo to your mission folder.

3. Download the <code>stringTable.xml</code> file linked below from the [Community Localization GitHub](https://github.com/oiad/communityLocalizations) and copy it to your mission folder, it is a community based localization file and contains translations for major community mods including this one.

**[>> Download stringTable.xml <<](https://github.com/oiad/communityLocalizations/blob/master/stringTable.xml)**

# dayz_server install:

1. Copy the <code>dayz_server\compile\server_changeCode.sqf</code> file from the repo to your <code>dayz_server\compile</code> folder

2. In your <code>dayz_server\init\server_functions.sqf</code> file, find this line:
	```sqf
	spawn_vehicles = compile preprocessFileLineNumbers "\z\addons\dayz_server\compile\spawn_vehicles.sqf";
	```
	Add the following after it:
	```sqf
	
	call compile preprocessFileLineNumbers "\z\addons\dayz_server\compile\server_changeCode.sqf";
	```

# Battleye filters:

1. In your config\<yourServerName>\Battleye\publicVariable.txt around line 2 find the line starting with: <code>5 !=(remExField|remExFP)</code> add this to the end of the line:

	```sqf
	!=SK_changeCode
	```

	So it will then look like this for example:

	```sqf
	5 !=(remExField|remExFP) <CUT> !=SK_changeCode
	```
	
2. In your config\<yourServerName>\Battleye\scripts.txt around line 19 find the line starting with: <code>5 createDialog !="_region = createDialog \"RscDisplaySpawnSelecter\";"</code> add this to the end of the line:

	```sqf
	!"createDialog _dialog;\n\nwaitUntil {!dialog};\n\nif (keypadCancel) exitWith {"
	```

	So it will then look like this for example:

	```sqf
	5 createDialog !="_region = createDialog \"RscDisplaySpawnSelecter\";" <CUT> !"createDialog _dialog;\n\nwaitUntil {!dialog};\n\nif (keypadCancel) exitWith {"
	```

3. In your config\<yourServerName>\Battleye\scripts.txt around line 72 find the line starting with: <code>5 systemChat !="systemChat format[localize \"str_missing_to_do_this\", _x];"</code> add this to the end of the line:

	```sqf
	!"systemChat format[localize \"STR_CL_" !"systemChat localize \"STR_CL_"
	```

	So it will then look like this for example:

	```sqf
	5 systemChat !="systemChat format[localize \"str_missing_to_do_this\", _x];" <CUT> !"systemChat format[localize \"STR_CL_" !"systemChat localize \"STR_CL_"
	```