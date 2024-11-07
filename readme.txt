1.26 DayZ Chernarus Kamensk Mine Tunnel Bunker Mod For PC & Console, Changelog & Terms Of Use

Using the new restricted area method, when a player logs-off at the entrance to the lower mine tunnel entrance at Kamensk and logs back in, they are teleported
to the insides of a dark bunker complex which has military loot. Players then need to return to the entrance, log off, and when they log back in they are back at Kamensk.

The tunnel bunker is actually located in the sky to the East of Skalisky Island.

I have included the DayZ Editor PC DayZ Mod File so you can play around with the files and see how it's done. ( tunnel-test.dze ). This .DZE file includes the tunnel "creation" place at the NEAF & the Bunker in the sky near Skalisky.

Limited Testing on PC Chernarus Local Server & Xbox Remote Server Version 1.26 OCT 2024.

Thanks to @King_Alobar_& JinieJ for the idea!

Created by @scalespeeder. Please report bugs & errors to scalespeeder@gmail.com with screenshots.

TERMS OF USE
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS
OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN
AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH
THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Using these modded xml & json files could break the functioning of your DAYZ server, requiring a reinstall that would wipe
all player progress.

Using these modded xml & json  files neccessitates increased regular restarts to prevent server crashing.

It is suggested you thoroughly test your server after applying these files to ensure proper
functioning of your server.

Please note that if the server is full & a log-on queue is in effect, the player will be at the back of that queue.

INSTRUCTIONS

Download these files from my Github or Mega. On github click on the green "Code" button & "download zip". On Mega click on the green "download" button & "download as a zip file".
Save the files in their own folder somewhere easily accesible on your PC.

-----

It's best to download files & edit locally on your PC if you can.

Check all edits with an online XML validator: https://www.xmlvalidation.com/ & for JSON: https://jsonformatter.curiousconcept.com/

STOP YOUR SERVER

-----

Ensure your DayZ Server has activated the cfggameplay.json. For console users on Nitrado Servers, go to "General Settings" on your server and tick "Enable cfggameplay.json" & save.

On PC Servers add or edit the following line to your serverDZ.cfg:

enableCfgGameplayFile = 1;

(On some PC servers, including Nitrado, the serverDZ.cfg is "hidden", so you need to enable "expert mode" in settings,
then go to "expert settings", which is the serverDZ.cfg. Stop the server before making changes this way.)

-----

On console, go to your Nitrado dashboard, then to your server, then to the file-browser, then to the "custom" folder, and upload "teleport-kamensk-to-tunnel.json" "teleport-tunnel-to-kamensk.json"
& "Kamensk-Tunnel-Objects.json"

On PC, create a custom folder inside your mission file, (eg mpmissions\dayzOffline.chernarusplus\custom )then repeat the above uploads.

The "Kamensk-Tunnel-Objects.json" file adds the tunnel-bunker to the map.

The 2 "teleport" json files tell the server where the fast travel points are, and where the player should teleport to.

Next, upload the "cfgundergroundtriggers.json" to your mission folder (eg mpmissions\dayzOffline.chernarusplus ), replacing the original one

OR if you already are using darkness underground triggers in your Chernarus Server, add this trigger to your file:

{ 	 
			"Position": [ 14366.71, 193.51, 3286.10],
			"Orientation": [ 112.09698486328125, 0, 0 ],
			"Size": [ 100, 100, 100 ],
			"EyeAccommodation": 0,
			"Breadcrumbs": [],
			"InterpolationSpeed": 1
		}
		
(Remember to add a comma after the } eg }, if the trigger is inserted into a list of triggers)


The underground trigger file makes it dark in the bunker tunnel. If you want a lit tunnel, don't use it.

-----

Next, open your cfggameplay.json file and after

"wetnessWeightModifiers": [1.0, 1.0, 1.33, 1.66, 2.0] add a comma to the end, so it looks like this:

"wetnessWeightModifiers": [1.0, 1.0, 1.33, 1.66, 2.0],

then paste in this line:

"playerRestrictedAreaFiles": ["custom/teleport-kamensk-to-tunnel.json","custom/teleport-tunnel-to-kamensk.json"]

The section should now look something like this:

"WorldsData":
		{
		"lightingConfig": 0,
		"objectSpawnersArr": [],
		"environmentMinTemps": [-3, -2, 0, 4, 9, 14, 18, 17, 13, 11, 9, 0],
		"environmentMaxTemps": [3, 5, 7, 14, 19, 24, 26, 25, 18, 14, 10, 5],
		"wetnessWeightModifiers": [1.0, 1.0, 1.33, 1.66, 2.0],
		"playerRestrictedAreaFiles": ["custom/teleport-kamensk-to-tunnel.json","custom/teleport-tunnel-to-kamensk.json"]
	},

We are actually taking advantage of the code designed for the Sakhal Military Bunker, which on Sakhal is used to make sure you don't get stuck in
the bunker if the doors close - the server teleports you to a safe location when you log off & on. We can use this to create our fast travel teleport system.

-----

Next in the cfggameplay.json file look for the "objectSpawnersArr" line.

Edit it to look like this to spawn in the tunnel:

		"objectSpawnersArr": ["custom/Kamensk-Tunnel-Objects.json"],
	
If you already refer to some custom object spawner files, it should look something like this:

	"objectSpawnersArr": ["custom/Kamensk-Tunnel-Objects.json","custom/some-other-file-name.json"],
	
	
remember to save and re-upload if you need to.
 	
-----

Next we need to add the code to make loot spawn in the bunker part of the tunnel.

Locate your mapgroupos.xml file in your mission folder (eg mpmissions\dayzOffline.chernarusplus )

& near the top, below <map> add the following line:

<group name="Land_Underground_Storage_POX" pos="14398.425781 193.504623 3254.571045" rpy="0.000000 0.000000 -158.115448" a="-111.885"/>

remember to save and re-upload if you need to.

Locate your mapgrouproto.xml file in your mission folder (eg mpmissions\dayzOffline.chernarusplus )

& near the top, below 	</defaults> add the following lines:

<group name="Land_Underground_Storage_POX" lootmax="10">
			
				<usage name="Military" />
			
				<container name="lootFloor" lootmax="10">
						<category name="containers" />
						<category name="clothes" />
						<category name="weapons" />
						<category name="explosives" />
						<point pos="-2.667725 0.745178 0.938353" range="0.340625" height="0.851563" flags="16" />
						<point pos="-1.363281 1.730652 0.113769" range="0.203125" height="0.507813" />
						<point pos="-1.726439 1.730652 3.882813" range="0.237500" height="0.593750" />
						<point pos="-1.590088 1.730652 -1.161133" range="0.271875" height="0.679688" />
						<point pos="5.422607 1.501953 -2.364990" range="0.306250" height="0.765625" />
						<point pos="-7.669434 0.958984 -3.243410" range="0.650000" height="1.625000" />
						<point pos="7.447265 1.130554 -2.233886" range="0.375000" height="0.937500" />
						<point pos="-3.325440 1.730652 2.102783" range="0.375000" height="0.937500" />
						<point pos="-5.305054 2.138062 1.946287" range="0.375000" height="0.937500" />
						<point pos="2.062988 1.151733 0.381348" range="0.409375" height="1.023438" />
						<point pos="-3.639160 0.745178 0.901490" range="0.409375" height="1.023438" flags="16" />
						<point pos="-6.067993 1.115967 -2.867005" range="0.271875" height="0.679688" flags="16" />
						<point pos="4.395263 1.109497 -2.981445" range="0.203125" height="0.507813" flags="16" />
				</container>
				<dispatch dechance="1.000000">
						<proxy type="Grenade_ChemGas" pos="-3.30603 0.26218 -1.340943" rpy="0.000000 0.000000 0.000000" dechance="0.25" />
						<proxy type="Grenade_ChemGas" pos="-3.25939 0.26218 -1.119508" rpy="0.000000 0.000000 0.000000" dechance="0.25" />
						<proxy type="Grenade_ChemGas" pos="4.810425 2.198035 0.923217" rpy="0.000000 0.000000 0.000000" dechance="0.25" />
						<proxy type="Grenade_ChemGas" pos="4.863892 2.198035 1.143250" rpy="0.000000 0.000000 0.000000" dechance="0.25" />
				</dispatch>
		</group>
		
remember to save and re-upload if you need to.

-----	


If you'd like to make the logging off & on process faster for your players, open your globals.xml file, find the login / logoff timers and edit them
to look like this:

 <var name="TimeLogin" type="0" value="5"/>
 <var name="TimeLogout" type="0" value="5"/>
 
remember to save and re-upload if you need to.
 
-----

Now you can just re-start your server and the tunnel bunker system will be in place. Enjoy!

Thanks, Rob.
