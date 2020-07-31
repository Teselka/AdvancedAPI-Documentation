# AdvancedAPI-Documentation
Documentation for nixware.cc AdvancedAPI lua

## How to use
Move AdvancedAPI.lua in directory Steam directory/steamapps/common/Counter-Strike Global Offensive/lua

## Script globals
ADVANCED_API_VERSION = 1.3; -- Current AdvancedAPI version

## Available netvars
- m_fFlags
- m_iHealth
- m_iTeamNum
- m_hActiveWeapon
- m_vecOrigin
- m_angEyeAngles
- m_flSimulationTime
- m_flOldSimulationTime
- m_lifeState
- m_bPinPulled
- m_fThrowTime
- m_flLowerBodyYawTarget
- m_bGunGameImmunity
- m_flFlashDuration
- m_bIsScoped
- m_flNextAttack
- m_zoomLevel
- m_Collision
- m_flDuckSpeed
- m_flDuckAmount
- m_iClip1
- m_iClip2
- m_fAccuracyPenalty
- m_flPostponeFireReadyTime
- m_flNextPrimaryAttack   -- Hazedumper
- m_flNextSecondaryAttack -- Hazedumper
- m_iShotsFired           -- Hazedumper
- m_iItemDefinitionIndex  -- Hazedumper
- m_vecViewOffset         -- Hazedumper
- m_nTickBase             -- Hazedumper
- m_MoveType              -- Hazedumper
- m_vecVelocity(Lua table, has 3 positions 0, 1, 2)

## Math variables
- NULL = 0
- M_PI = 3.14159265358979323846  -- PI Number
- M_180_PI = 0.0174533  -- PI Number, divided by 180
- M_PI_180 = 57.2958    -- PI Number, multiplicated by 180
- INT_MAX  = 2147483647 -- From C/C++ library
- INFINITE = math.huge  -- Infinte number from lua math library

## Math functions
### round(x) - Rounding a number
x - Number for rounding
```

local x = round(1.5); -- returns integer
```
### hasbit(x, p) - Checking if number has a specific bit 
- x - Number
- p - Sought bit
```

local Flags = LocalPlayer:get_prop_int(m_fFlags);
local OnGround = hasbit(Flags, FL_ONGROUND); -- returns boolean
```

### clamp(x, min, max) - Clamping x value
- x   - Number for clamping
- min - Min number value
- max - Max number value
```
local x = clamp(5, 0, 4); -- returns integer
```
### IsInfinite(x) - Checking if number is infinite
- x - number for checking
```
local IsInf = IsInfinite(INFINITE); -- returns boolean
```

### IsNaN(x) -- Checking if number is NaN
- x - Number for checking
```
local NaN = 0/0;
local isnan = IsNaN(NaN) -- returns boolean
```

### NormalizePitch(pitch) -- Normalizing pitch angle (Only for player's viewangles)
- pitch - Pitch for normalizing
```
local NormalizedPitch = NormalizePitch(-INT_MAX); -- returns integer
```

### NormalizeYaw(yaw) -- Normalizing yaw angle (Only for player's viewangles)
- yaw - Yaw for normalizing
```
local NormalizedYaw = NormalizeYaw(-INT_MAX); -- returns integer
```

### NormalizeRoll(roll) -- Normalizing roll angle (Only for player's viewangles)
- roll - Roll for normalizing
```
local NormalizedRoll = NormalizeRoll(-INT_MAX); -- returns integer
```

### NormalizeAngle(vAngle) -- Normalizing angle_t (aka Valve's QAngle) (Only for player's viewangles)
- vAngle - Angle for normalizing 
```
local NormalizedAngle = angle_t.new(-INFINITE, INFINITE, 0); -- returns angle_t object
```

### NormalizeVector(vAngle) -- Normalizing vec3_t (Only for player's viewangles) (Same as NormalizeAngle, just vector object)
- vAngle - Vector for normalizing 
```
local NormalizedVector = vec3_t.new(-INFINITE, INFINITE, 0); -- returns vec3_t object
```

### VectorAddition(vFirst, vSecond) -- Additing second vector to first
- vFirst - Vector for addition
- vSecond - Vector what is being addited
```
local vFirst = vec3_t.new(59, 15.54, 84);
local vSecond = vec3_t.new(415, 36, 18.48155);
local Addited = VectorAddition(vFirst, vSecond); -- return vec3_t object
```

### VectorSubtraction(vFirst, vSecond) -- Subtracting second vector from first
- vFirst - Vector for subtraction
- vSecond - Vector what is being subtracted
```
local vFirst = vec3_t.new(75.12, 87, 84);
local vSecond = vec3_t.new(415.5, 36.2, 18.48155);
local Subtracted = VectorSubtraction(vFirst, vSecond); -- return vec3_t object
```

### VectorDivision(vFirst, vSecond) -- Dividing second vector on first
- vFirst - Vector for dividing
- vSecond - Vector on what is being divided
```
local vFirst = vec3_t.new(5249, 1542, 8486);
local vSecond = vec3_t.new(13, 12, 24);
local Divided = VectorDivision(vFirst, vSecond); -- return vec3_t object
```

### VectorMultiplication(vFirst, vSecond) -- Multiplicating second vector on first
- vFirst - Vector for multiplication
- vSecond - Vector on what is being multiplicated
```
local vFirst = vec3_t.new(24, 14, 86);
local vSecond = vec3_t.new(18, 24, 12);
local Multiplicated = VectorMultiplication(vFirst, vSecond); -- return vec3_t object
```

### VectorNumberSubtraction(Vector, Number) -- Subtracting number from vector
- Vector - Vector for subtraction
- Number what is being subtracted
```
local Vector = vec3_t.new(54, 1, 6);
local Number = vec3_t.new(26, 0.5, 7);
local Subtracted = VectorNumberSubtraction(Vector, Number); -- return vec3_t object
```

### VectorNumberAddition(Vector, Number) -- Additing number to vector
- Vector - Vector for additing
- Number what is being addited
```
local Vector = vec3_t.new(42, 0, 0);
local Number = vec3_t.new(10, 2, 4);
local Addited = VectorNumberAddition(Vector, Number); -- return vec3_t object
```

### VectorNumberDivision(Vector, Number) -- Dividing number on vector
- Vector - Vector for dividing
- Number what is being divited
```
local Vector = vec3_t.new(42, 14, 87);
local Number = vec3_t.new(5, 6, 9);
local Divided = VectorNumberDivision(Vector, Number); -- return vec3_t object
```

### VectorNumberMultiplication(Vector, Number) -- Multiplicating number on vector
- Vector - Vector for multiplication
- Number what is being multiplicated
```
local Vector = vec3_t.new(98, 11, 48);
local Number = vec3_t.new(1, 4, 9);
local Multiplicated = VectorNumberMultiplication(Vector, Number); -- returns vec3_t object
```

### GetMiddlePoint(vFirst, vSecond) -- Calculating middle point between two vectors
- vFirst - Vector first
- vSecond - Vector second
```
local vSource = VectorAddition(LocalPlayer:get_prop_vector(m_vecOrigin), LocalPlayer:get_prop_vector(m_vecViewOffset));
local vDest = VectorAddition(Teammate:get_prop_vector(m_vecOrigin), Teammate:get_prop_vector(m_vecViewOffset));
local MiddlePoint = GetMiddlePoint(vSource, vDest); -- returns vec3_t object
```

### CalcAngle(vecSource, vecDestination) -- Calculating viewangles to aim at target vector
- vecSource - Vector (Forces vector if used angle_t) from we want to aim
- vecDestination - Vector (Forces vector if used angle_t) on what we want to aim
```
local vecSource = VectorAddition(LocalPlayer:get_prop_vector(m_vecOrigin), LocalPlayer:get_prop_vector(m_vecViewOffset));
local vecDestination = Entity:get_player_hitbox_pos(HITBOX_HEAD);
local vCalculated = CalcAngle(vecSource, vecDestination); -- returns vec3_t object
```

### AngleVectors(vAngles) -- Converts a QAngle into either one or three normalised Vectors
- vAngles - Vector (Forces vector if used angle_t) what we want to convert
```
local vAngles = vec3_t.new(21, 78, 0);
local Vector = AngleVectors(vAngles); -- returns vec3_t object
```

### VectorAngles(vAngles) -- Converts a single Vector into a QAngle
- vAngles - Vector (Forces vector if used angle_t) what we want to convert
```
local vAngles = vec3_t.new(37, 59, 4884);
local Vector = AngleVectors(vAngles); -- returns vec3_t object
```

### GetMaxDesyncDelta(Entity) -- Calculating max desync delta of entity
- Entity - entity_t what we want to get delta
```
local LocalPlayer = entitylist:get_local_player();
local MaxDesync = GetMaxDesyncDelta(LocalPlayer); -- returns float
```

### RAD2DEG(x) -- Converting radians to degrees
- x - Radians what we want to convert
```
local Degrees = RAD2DEG(3.14); -- returns float
```

### DEG2RAD(x) -- Converting degrees to radians
- x - Degrees what we want to convert
```
local Radians = DEG2RAD(180); -- returns float
```

### VectorDot(vFirst, vSecond) -- Calculating the dot product of two vectors
- vFirst  - The first vector
- vSecond - The second vector
```
local vFirst = vec3_t.new(13, 37, 14);
local vSecond = vec3_t.new(88, 100, 7);
local DotProduct = VectorDot(vFirst, vSecond); -- returns float
```

### VectorLengthSqr(Vector) -- Calculating vector squares length
- Vector - Vector we want to convert
```
local Vector = vec3_t.new(54, 87, 966);
local LengthSqr = VectorLengthSqr(Vector); -- returns float
```

### GetFov(viewAngle, aimAngle) -- Calculating fov from first vector to second
- viewAngle - Vector (Forces vector if used angle_t) first angle
- aimAngle  - Vector (Forces vector if used angle_t) second angle
```
local LocalPlayer = entitylist:get_local_player();
local vSource = VectorAddition(LocalPlayer:get_prop_vector(m_vecOrigin), LocalPlayer:get_prop_vector(m_vecViewOffset));
local vDestination = Entity:get_player_hitbox_pos(0);
local aimAngle = CalcAngle(vSource, vDestination);
local viewAngle = vec3_t.new(pCmd.pitch, pCmd.yaw, pCmd.roll);
local Fov = GetFov(viewAngle, aimAngle);
```

### Distance3D(vFirst, vSecond) -- Calculating distance between two 3D vectors
- vFirst  - Vector  what we want to convert
- vSecond - Vector what we want to convert
```
local LocalPlayer = entitylist:get_local_player();
local vFirst = VectorAddition(LocalPlayer:get_prop_vector(m_vecOrigin), LocalPlayer:get_prop_vector(m_vecViewOffset));
local vSecond = Entity:get_player_hitbox_pos(HITBOX_HEAD);
local Distance = Distance3D(vFirst, vSecond); -- returns float
```

### Distance2D(vFirst, vSecond) -- Calculating distance between two 2D vectors
- vFirst  - Vector2D  what we want to convert
- vSecond - Vector2D what we want to convert
```
local vFirst  = vec2_t.new(0, 0);
local vSecond = vec2_t.new(100, 100);
local Distance = Distance2D(vFirst, vSecond); -- returns float
```

### GetCurtime(Player) -- Calclulating curtime of player
- Player - entity_t what we want to get curtime
```
local LocalPlayer = entitylist:get_local_player();
local Curtime = GetCurtime(LocalPlayer); -- return flaot
```

### GetTickrate() -- Calculating server tickrate
```
local Tickrate = GetTickrate();
```

### TIME_TO_TICKS(dt) -- Converting time to ticks
- dt - Time what we want to convert
```
local Ticks = TIME_TO_TICKS(TargetEntity:get_prop_float(m_flSimulationTime) + GetLerpTime()); -- returns float
```

### TICKS_TO_TIME(t) -- Converting ticks to time
- t - Ticks waht we want to convert
```
local Time = TICKS_TO_TIME(GetLerpTime()); -- returns float
```

### GetLerpTime() -- Calculating server lerp time
```
local LerpTime = GetLerpTime();
```

### RotateMovement(pCmd, vAngles) -- Rotating movement into vAngles direction
- pCmd - usercmd_t needed to get forward, sidemoves and viewangles
- vAngles - Vector (Forces vector if used angle_t) in what we want to go
```
local LocalPlayer = entitylist:get_local_player();
local vSource = VectorAddition(LocalPlayer:get_prop_vector(m_vecOrigin), LocalPlayer:get_prop_vector(m_vecViewOffset));
local vAngles = VectorAngles(VectorSubtraction(Entity:get_player_hitbox_pos(HITBOX_HEAD), vSource));
vAngles = NormalizeVector(vAngles);
pCmd.forwardmove = 250;
RotateMovement(pCmd, vAngles);
```

### ApproachAngle(target, value, speed) -- From ValveSDK, no description :(
#### https://github.com/ValveSoftware/source-sdk-2013/blob/0d8dceea4310fde5706b3ce1c70609d72a38efdf/sp/src/mathlib/mathlib_base.cpp#L3438
- target - float value
- value - float value
- speed - float value
```
local m_flGoalFeetYaw = ApproachAngle(m_flEyeYaw, m_flGoalFeetYaw, ((m_flStopToFullRunningFraction * 20.0) + 30.0) * m_iLastClientSideAnimationUpdateFramecount);
-- returns float
```

### AngleDifference(destAngle, srcAngle) -- From ValveSDK, getting delta between two angles
#### https://github.com/ValveSoftware/source-sdk-2013/blob/master/sp/src/mathlib/mathlib_base.cpp#L3466
- destAngle - float first angle
- srcAngle - float second angle
```
local Delta = AngleDifference(m_flGoalFeetYaw, LowerBodyYaw); -- returns float
```



## Helper functions
### HasC4(Player) -- Checking if player has c4
- Player - entity_t what we want to check
```
local LocalPlayer = entitylist:get_local_player();
local C4 = HasC4(LocalPlayer);
```

### GetWeaponData(Weapon) -- Getting WeaponInfo_t struct of weapon
- Weapon - entity_t active weapon what from we want to get struct
```
local LocalPlayer = entitylist:get_local_player();
local ActiveWeaponHandle = LocalPlayer:get_prop_int(m_hActiveWeapon);
local Weapon = entitylist.get_entity_from_handle(ActiveWeaponHandle);
local WeaponData = GetWeaponData(Weapon); -- returns cdata<int*> object
```

### IsKnife(Weapon) -- Checking if weapon is knife
- Weapon - entity_t active weapon what we want to check
```
local LocalPlayer = entitylist:get_local_player();
local ActiveWeaponHandle = LocalPlayer:get_prop_int(m_hActiveWeapon);
local Weapon = entitylist.get_entity_from_handle(ActiveWeaponHandle);
local Knife = IsKnife(Weapon); -- returns boolean
```

### IsNade(Weapon) -- Checking if weapon is nade
- Weapon - entity_t active weapon what we want to check
```
local LocalPlayer = entitylist:get_local_player();
local ActiveWeaponHandle = LocalPlayer:get_prop_int(m_hActiveWeapon);
local Weapon = entitylist.get_entity_from_handle(ActiveWeaponHandle);
local Nade = IsNade(Weapon); -- returns boolean
```

## Exploits
### IsExploitRecharged(LocalPlayer, Weapon, Exploit) -- Checking if one of exploits is recharged 
#### Shift values from https://yougame.biz/threads/134913/
- LocalPlayer - entity_t local player
- Weapon - entity_t  active weapon
- Exploit - exploit what we want to know recharge
```
local LocalPlayer = entitylist:get_local_player();	
local ActiveWeaponHandle = LocalPlayer:get_prop_int(m_hActiveWeapon);
local Weapon = entitylist.get_entity_from_handle(ActiveWeaponHandle);
local IsRecharged = IsExploitRecharged(LocalPlayer, Weapon, ui.get_int("ragebot_active_exploit")); -- returns boolean
```

### GetExploitCharge(LocalPlayer, Weapon, Exploit) -- Calcuating exploit charge time
- LocalPlayer - entity_t local player
- Weapon - entity_t  active weapon
- Exploit - exploit what we want to know recharge
```
local LocalPlayer = entitylist:get_local_player();	
local ActiveWeaponHandle = LocalPlayer:get_prop_int(m_hActiveWeapon);
local Weapon = entitylist.get_entity_from_handle(ActiveWeaponHandle);
local Recharge = GetExploitCharge(LocalPlayer, Weapon, ui.get_int("ragebot_active_exploit")); -- returns float
-- returns 0 if exploit is charged
```

## Libraries
### Timers lib https://nixware.cc/threads/7591/
#### Timer.new_timeout(callback, ms) -- Executes function on end of the timer only once
- callback - Function what we want execute at end of the timer
- ms - integer delay before executing
```
Timer.new_timeout(function()
   client.notify("Executed!");
end, 1000);
```

#### Timers.new_interval(callback, ms) -- Executes function on end of the timer and repeating again
- callback - Function what we want execute at end of the timer
- ms - integer delay before executing
```
Timer.new_interval(function()
   client.notify("Executed!");
end, 1000);
```

#### Timers.listener() -- Listen for all timers (needed for executing it)
```
client.register_callback("paint", function()
	Timer.listener();
end);
```

## Structures and enums
### WeaponInfo_t -- Not finished yet, because brain issue
```
WEAPDATA_MAX_CLIP = 0x05;
WEAPDATA_MAX_RESERVED_AMMO = 0x09; -- Max clip 2
WEAPDATA_TYPE = 0x28;
WEAPDATA_COST = 0x34;
-- Here should be reward, but i have some issues with brain
WEAPDATA_DAMAGE = 0x60;
WEAPDATA_ARMORRATIO = 0x64; -- float
WEAPDATA_BULLETS = 0x68; -- I think, that's unused
WEAPDATA_PENETRATION = 0x72; -- float
```


### MoveType_t
```
MOVETYPE_NONE = 0; -- Freezes the entity, outside sources can't move it. 
MOVETYPE_ISOMETRIC = 1; -- For players in TF2 commander view etc. Do not use this for normal players! 
MOVETYPE_WALK = 2; -- Default player (client) move type. 
MOVETYPE_STEP = 3; -- NPC movement 
MOVETYPE_FLY = 4; -- Fly with no gravity. 
MOVETYPE_FLYGRAVITY = 5; -- Fly with gravity. 
MOVETYPE_VPHYSICS = 6; -- Physics movetype (prop models etc.) 
MOVETYPE_PUSH = 7; -- No clip to world, but pushes and crushes things.
MOVETYPE_NOCLIP = 8; -- Noclip, behaves exactly the same as console command.
MOVETYPE_LADDER = 9; -- For players, when moving on a ladder. 
MOVETYPE_OBSERVER = 10; -- Spectator movetype. DO NOT use this to make player spectate. 
MOVETYPE_CUSTOM = 11; -- Custom movetype, can be applied to the player to prevent the default movement code from running, while still calling the related hooks
MOVETYPE_LAST = MOVETYPE_CUSTOM;
MOVETYPE_MAX_BITS = 4;
```

### Buttons
```
IN_ATTACK   = 1;       --  (1 << 0)  -- Fire weapon
IN_JUMP     = 2;       --  (1 << 1)  -- Jump
IN_DUCK     = 4;       --  (1 << 2)  -- Crouch
IN_FORWARD  = 8;       --  (1 << 3)  -- Walk forward
IN_BACK     = 16;      --  (1 << 4)  -- Walk backwards
IN_USE      = 32;      --  (1 << 5)  -- Use (Defuse bomb, etc...)
IN_CANCEL   = 64;      --  (1 << 6)
IN_LEFT     = 128;     --  (1 << 7)  -- Walk left
IN_RIGHT    = 256;     --  (1 << 8)  -- Walk right
IN_MOVELEFT = 512;     --  (1 << 9)
IN_MOVERIGHT= 1024;    --  (1 << 10)
IN_ATTACK2  = 2048;    --  (1 << 11) -- Secondary fire (Revolver, Glock change fire mode, Famas change fire mode), zoom
IN_RUN      = 4096;    --  (1 << 12)
IN_RELOAD   = 8192;    --  (1 << 13) -- Reload weapon
IN_ALT1     = 16384;   --  (1 << 14)
IN_ALT2     = 32768;   --  (1 << 15)
IN_SCORE    = 65536;   --  (1 << 16) -- Used by client.dll for when scoreboard is held down
IN_SPEED    = 131072;  --  (1 << 17) -- Player is holding the speed key
IN_WALK     = 262144;  --  (1 << 18) -- Player holding walk key
IN_ZOOM     = 524288;  --  (1 << 19) -- Zoom key for HUD zoom
IN_WEAPON1  = 1048576; --  (1 << 20) -- weapon defines these bits
IN_WEAPON2  = 2097152; --  (1 << 21) -- weapon defines these bits
IN_BULLRUSH = 4194304; --  (1 << 22)
IN_GRENADE1 = 8388608; --  (1 << 23) -- grenade 1
IN_GRENADE2 = 16777216;--  (1 << 24) -- grenade 2
IN_ATTACK3  = 33554432;--  (1 << 25)
```

## EntityFlags
```
FL_ONGROUND  = 1;  -- (1 << 0), At rest / on the ground
FL_DUCKING   = 2;  -- (1 << 1), Player flag -- Player is fully crouched
FL_ANIMDUCKING=4;  -- (1 << 2), Player flag -- Player is in the process of crouching or uncrouching but could be in transition
--		                                       Fully ducked:  FL_DUCKING &  FL_ANIMDUCKING
--           Previously fully ducked, unducking in progress:  FL_DUCKING & !FL_ANIMDUCKING
--                                           Fully unducked: !FL_DUCKING & !FL_ANIMDUCKING
--           Previously fully unducked, ducking in progress: !FL_DUCKING &  FL_ANIMDUCKING
FL_WATERJUMP = 8;  -- (1 << 3), Player jumping out of water
FL_ONTRAIN   = 16; -- (1 << 4), Player is _controlling_ a train, so movement commands should be ignored on client during prediction.
FL_INRAIN	   = 32; -- (1 << 5), Indicates the entity is standing in rain
FL_FROZEN    = 64; -- (1 << 6), Player is frozen for 3rd person camera
FL_ATCONTROLS= 128;-- (1 << 7), Player can't move, but keeps key inputs for controlling another entity
FL_CLIENT	   = 256;-- (1 << 8), Is a player
FL_FAKECLIENT= 512;-- (1 << 9), Fake client, simulated server side; don't send network messages to them
-- NON-PLAYER SPECIFIC (i.e., not used by GameMovement or the client .dll ) -- Can still be applied to players, though
FL_INWATER = 1024; -- (1 << 10), // In water
```

### ClientFrameStage_t
```
FRAME_UNDEFINED = -1;	-- Haven't run any frames yet
FRAME_START = 0;
FRAME_NET_UPDATE_START = 1;	-- A network packet is being recieved
FRAME_NET_UPDATE_POSTDATAUPDATE_START = 2;-- Data has been received and we're going to start calling PostDataUpdate
FRAME_NET_UPDATE_POSTDATAUPDATE_END = 3;	-- Data has been received and we've called PostDataUpdate on all data recipients
FRAME_NET_UPDATE_END = 4;	-- We've received all packets, we can now do interpolation, prediction, etc..
FRAME_RENDER_START = 5;	-- We're about to start rendering the scene
FRAME_RENDER_END = 6;	-- We've finished rendering the scene.
```

### ItemDefinitionIndex
```
WEAPON_NONE = 0;
WEAPON_DEAGLE = 1;
WEAPON_ELITE = 2;
WEAPON_FIVESEVEN = 3;
WEAPON_GLOCK = 4;
WEAPON_AK47 = 7;
WEAPON_AUG = 8;
WEAPON_AWP = 9;
WEAPON_FAMAS = 10;
WEAPON_G3SG1 = 11;
WEAPON_GALILAR = 13;
WEAPON_M249 = 14;
WEAPON_M4A1 = 16;
WEAPON_MAC10 = 17;
WEAPON_P90 = 19;
WEAPON_MP5SD = 23;
WEAPON_UMP45 = 24;
WEAPON_XM1014 = 25;
WEAPON_BIZON = 26;
WEAPON_MAG7 = 27;
WEAPON_NEGEV = 28;
WEAPON_SAWEDOFF = 29;
WEAPON_TEC9 = 30;
WEAPON_TASER = 31;
WEAPON_HKP2000 = 32;
WEAPON_MP7 = 33;
WEAPON_MP9 = 34;
WEAPON_NOVA = 35;
WEAPON_P250 = 36;
WEAPON_SHIELD = 37;
WEAPON_SCAR20 = 38;
WEAPON_SG556 = 39;
WEAPON_SSG08 = 40;
WEAPON_KNIFEGG = 41;
WEAPON_KNIFE = 42;
WEAPON_FLASHBANG = 43;
WEAPON_HEGRENADE = 44;
WEAPON_SMOKEGRENADE = 45;
WEAPON_MOLOTOV = 46;
WEAPON_DECOY = 47;
WEAPON_INCGRENADE = 48;
WEAPON_C4 = 49;
WEAPON_HEALTHSHOT = 57;
WEAPON_KNIFE_T = 59;
WEAPON_M4A1_SILENCER = 60;
WEAPON_USP_SILENCER = 61;
WEAPON_CZ75A = 63;
WEAPON_REVOLVER = 262208; -- 64
WEAPON_TAGRENADE = 68;
WEAPON_FISTS = 69;
WEAPON_BREACHCHARGE = 70;
WEAPON_TABLET = 72;
WEAPON_MELEE = 74;
WEAPON_AXE = 75;
WEAPON_HAMMER = 76;
WEAPON_SPANNER = 78;
WEAPON_KNIFE_GHOST = 80;
WEAPON_FIREBOMB = 81;
WEAPON_DIVERSION = 82;
WEAPON_FRAG_GRENADE = 83;
WEAPON_SNOWBALL = 84;
WEAPON_BUMPMINE = 85;
WEAPON_BAYONET = 500;
WEAPON_KNIFE_TACTICAL = 509;
WEAPON_KNIFE_SURVIVAL_BOWIE = 514;
WEAPON_KNIFE_PUSH = 516;
WEAPON_KNIFE_GYPSY_JACKKNIFE = 520;
WEAPON_KNIFE_WIDOWMAKER = 523;
WEAPON_KNIFE_BAYONET = 590324;
WEAPON_KNIFE_FLIP = 590329;
WEAPON_KNIFE_GUT = 590330;
WEAPON_KNIFE_KARAMBIT = 590331;
WEAPON_KNIFE_M9_BAYONET = 590332;
WEAPON_KNIFE_HUNTSMAN = 590333;
WEAPON_KNIFE_FALCHION = 590336;
WEAPON_KNIFE_BOWIE = 590338;
WEAPON_KNIFE_BUTTERFLY = 590339;
WEAPON_KNIFE_SHADOW_DAGGERS = 590340;
WEAPON_KNIFE_URSUS = 590343;
WEAPON_KNIFE_NAVAJA = 590344;
WEAPON_KNIFE_STILETTO = 590346;
WEAPON_KNIFE_TALON = 590347;
WEAPON_KNIFE_CSS = 590327;
WEAPON_KNIFE_CORD = 590341;
WEAPON_KNIFE_CANIS = 590342;
WEAPON_KNIFE_OUTDOOR = 590345;
WEAPON_KNIFE_SKELETON = 590349;
```

### Hitboxes
```
HITBOX_HEAD = 0;
HITBOX_NECK = 1;
HITBOX_PELVIS = 2;
HITBOX_STOMACH = 3;
HITBOX_THORAX = 4;
HITBOX_CHEST = 5;
HITBOX_UPPER_CHEST = 6;
HITBOX_RIGHT_THIGH = 7;
HITBOX_LEFT_THIGH = 8;
HITBOX_RIGHT_CALF = 9;
HITBOX_LEFT_CALF = 10;
HITBOX_RIGHT_FOOT = 11;
HITBOX_LEFT_FOOT = 12;
HITBOX_RIGHT_HAND = 13;
HITBOX_LEFT_HAND = 14;
HITBOX_RIGHT_UPPER_ARM = 15;
HITBOX_RIGHT_FOREARM = 16;
HITBOX_LEFT_UPPER_ARM = 17;
HITBOX_LEFT_FOREARM = 18;
HITBOX_MAX = 19;
```
