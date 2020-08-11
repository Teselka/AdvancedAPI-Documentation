# AdvancedAPI-Documentation
Documentation for nixware.cc AdvancedAPI lua

## How to use
Move AdvancedAPI.lua in directory Steam directory/steamapps/common/Counter-Strike Global Offensive/lua

## Script globals
ADVANCED_API_VERSION = 1.5; -- Current AdvancedAPI version

## Available netvars
- m_fFlags
- m_iHealth
- m_iTeamNum
- m_hActiveWeapon
- m_vecOrigin
- m_angEyeAngles
- m_flSimulationTime
- m_flOldSimulationTime
- m_iAccount
- m_bBombTicking
- m_flC4Blow
- m_nBombSite
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

## C Definitions
```
typedef void* FARPROC;
typedef void* HMODULE;
typedef const char* LPCSTR;
typedef wchar_t WCHAR;
typedef const WCHAR* LPCWSTR;
FARPROC GetProcAddress(HMODULE hModule, LPCSTR lpProcName);
HMODULE GetModuleHandleA(LPCSTR lpModuleName);

struct WeaponInfo_t
{
	char _0x0000[20];
	__int32 max_clip;	
	char _0x0018[12];
	__int32 max_reserved_ammo;
	char _0x0028[96];
	char* hud_name;			
	char* weapon_name;		
	char _0x0090[60];
	__int32 type;			
	__int32 price;			
	__int32 reward;			
	char _0x00D8[20];
	bool full_auto;		
	char _0x00ED[3];
	__int32 damage;			
	float armor_ratio;		 
	__int32 bullets;	
	float penetration;	
	char _0x0100[8];
	float range;			
	float range_modifier;	
	char _0x0110[16];
	bool silencer;			
	char _0x0121[15];
	float max_speed;		
	float max_speed_alt;
	char _0x0138[76];
	__int32 recoil_seed;
	char _0x0188[32];
};

typedef struct { 
	float x,y,z; 
} vec3_t; 
	
struct CBaseAnimState
{
	void* pThis;
	char pad2[91];
	void* pBaseEntity; 
	void* pActiveWeapon; 
	void* pLastActiveWeapon; 
	float m_flLastClientSideAnimationUpdateTime; 
	int m_iLastClientSideAnimationUpdateFramecount; 
	float m_flEyePitch; 
	float m_flEyeYaw; 
	float m_flPitch; 
	float m_flGoalFeetYaw; 
	float m_flCurrentFeetYaw;
	float m_flCurrentTorsoYaw; 
	float m_flUnknownVelocityLean;
	float m_flLeanAmount; 
	char pad4[4];
	float m_flFeetCycle;
	float m_flFeetYawRate;
	float m_fUnknown2;
	float m_fDuckAmount; 
	float m_fLandingDuckAdditiveSomething; 
	float m_fUnknown3;
	vec3_t m_vOrigin;
	vec3_t m_vLastOrigin; 
	float m_vVelocityX; 
	float m_vVelocityY;
	char pad5[4];
	float m_flUnknownFloat1;
	char pad6[8];
	float m_flUnknownFloat2;
	float m_flUnknownFloat3; 
	float m_flUnknown; 
	float speed_2d; 
	float flUpVelocity; 
	float m_flSpeedNormalized; 
	float m_flFeetSpeedForwardsOrSideWays; 
	float m_flFeetSpeedUnknownForwardOrSideways;
	float m_flTimeSinceStartedMoving; 
	float m_flTimeSinceStoppedMoving;
	unsigned char m_bOnGround; 
	unsigned char m_bInHitGroundAnimation;
	char pad7[10];
	float m_flLastOriginZ; 
	float m_flHeadHeightOrOffsetFromHittingGroundAnimation; 
	float m_flStopToFullRunningFraction; 
	char pad8[4];
	float m_flUnknownFraction; 
	char pad9[4];
	float m_flUnknown3;
	char pad10[528];
};
```

## Math variables
- NULL = 0
- M_PI = 3.14159265358979323846  -- PI Number
- M_PI_2 = 6.2831853071795862; -- PI Number, multiplicated by 2
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

### RandomFloat(min, max) - Returns random float, using vstdlib
- min - Min number value
- max - Max number value
```
local randflt = RandomFloat(0, 10); -- returns float
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

### Distance3D(vFirst, vSecond) -- Calculating distance between two 3D vectors (Since 1.4 verison returns smaller value)
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

## Renderer helpers
### IsOnScreen(Vector2D) -- Checking if vector2d is on screen
- Vector2D - vec2_t, what we want to know
```
local OnScreen = IsOnScreen(vec2_t.new(0, 0)); -- returns boolean
```

### DrawOutlined3DCircle(vOrigin, Radius, Segments, Color) -- Drawing circle on origin
- vOrigin - vec3_t, origin, where we want to draw circle
- Radius - int/float, circle radius
- Segments - int/float, circle segments
```
DrawOutlined3DCircle(vec3_t.new(0, 0, 0), 15, 30, color_t.new(255, 255, 255, 255));
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
local WeaponData = GetWeaponData(Weapon); -- returns cdata<WeaponInfo_t*> object
-- To use values from struct do WeaponData.{struct value}
```

### GetAnimstate(Player) -- Getting CBaseAnimState struct of player
- Player - entity_t what we want to get animstate
```
local LocalPlayer = entitylist:get_local_player();
local Animstate = GetAnimstate(LocalPlayer);
- To use values from struct do Animstate.{struct value}
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

### Bspflags
```
CONTENTS_EMPTY = 0; -- No contents
CONTENTS_SOLID = 0x1; -- an eye is never valid in a solid
CONTENTS_WINDOW = 0x2; -- translucent, but not watery (glass)
CONTENTS_AUX = 0x4;
CONTENTS_GRATE = 0x8; -- alpha-tested "grate" textures.  Bullets/sight pass through, but solids
CONTENTS_SLIME = 0x10;
CONTENTS_WATER = 0x20;
CONTENTS_BLOCKLOS = 0x40; -- block AI line of sight
CONTENTS_OPAQUE = 0x80;
LAST_VISIBLE_CONTENTS = 0x80 -- things that cannot be seen through (may be non-solid though)

ALL_VISIBLE_CONTENTS = bit32.band(LAST_VISIBLE_CONTENTS, (LAST_VISIBLE_CONTENTS-1));
CONTENTS_TESTFOGVOLUME = 0x100;
CONTENTS_UNUSED = 0x200;

-- unused
-- NOTE: If it's visible, grab from the top + update LAST_VISIBLE_CONTENTS
-- if not visible, then grab from the bottom.
CONTENTS_UNUSED6 = 0x400;
CONTENTS_TEAM1 = 0x800;
CONTENTS_TEAM2 = 0x1000;

-- ignore CONTENTS_OPAQUE on surfaces that have SURF_NODRAW
CONTENTS_IGNORE_NODRAW_OPAQUE = 0x2000

-- hits entities which are MOVETYPE_PUSH (doors, plats, etc.)
CONTENTS_MOVEABLE = 0x4000;

-- remaining contents are non-visible, and don't eat brushes
CONTENTS_AREAPORTAL = 0x8000;

CONTENTS_PLAYERCLIP = 0x10000;
CONTENTS_MONSTERCLIP = 0x20000;

-- currents can be added to any other contents, and may be mixed
CONTENTS_CURRENT_0 = 0x40000;
CONTENTS_CURRENT_90 = 0x80000;
CONTENTS_CURRENT_180 = 0x100000;
CONTENTS_CURRENT_270 = 0x200000;
CONTENTS_CURRENT_UP = 0x400000;
CONTENTS_CURRENT_DOWN = 0x800000;

CONTENTS_ORIGIN = 0x1000000 -- removed before bsping an entity

CONTENTS_MONSTER = 0x2000000 -- should never be on a brush, only in game
CONTENTS_DEBRIS =  0x4000000;
CONTENTS_DETAIL = 0x8000000; -- brushes to be added after vis leafs
CONTENTS_TRANSLUCENT = 0x10000000; -- auto set if any surface has trans
CONTENTS_LADDER = 0x20000000;
CONTENTS_HITBOX = 0x40000000; -- use accurate hitboxes on trace


-- NOTE: These are stored in a short in the engine now.  Don't use more than 16 bits
SURF_LIGHT = 0x0001; -- value will hold the light strength
SURF_SKY2D = 0x0002; -- don't draw, indicates we should skylight + draw 2d sky but not draw the 3D skybox
SURF_SKY = 0x0004; -- don't draw, but add to skybox
SURF_WARP = 0x0008; -- turbulent water warp
SURF_TRANS = 0x0010;
SURF_NOPORTAL = 0x0020; -- the surface can not have a portal placed on it
SURF_TRIGGER = 0x0040; -- FIXME: This is an xbox hack to work around elimination of trigger surfaces, which breaks occluders
SURF_NODRAW = 0x0080; -- don't bother referencing the texture

SURF_HINT = 0x0100; -- make a primary bsp splitter

SURF_SKIP = 0x0200; -- completely ignore, allowing non-closed brushes
SURF_NOLIGHT = 0x0400; -- Don't calculate light
SURF_BUMPLIGHT = 0x0800; -- calculate three lightmaps for the surface for bumpmapping
SURF_NOSHADOWS = 0x1000; -- Don't receive shadows
SURF_NODECALS = 0x2000; -- Don't receive decals
SURF_NOCHOP = 0x4000; -- Don't subdivide patches on this surface 
SURF_HITBOX = 0x8000; -- surface is part of a hitbox

-------------------------------------------------------
-- spatial content masks - used for spatial queries (traceline,etc.)
-------------------------------------------------------
MASK_ALL = (0xFFFFFFFF);
-- everything that is normally solid
MASK_SOLID = bit32.bor(CONTENTS_SOLID,  bit32.bor(CONTENTS_MOVEABLE,  bit32.bor(CONTENTS_WINDOW,  bit32.bor(CONTENTS_MONSTER, CONTENTS_GRATE))));
-- everything that blocks player movement
MASK_PLAYERSOLID = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_PLAYERCLIP, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_MONSTER,CONTENTS_GRATE)))));
-- blocks npc movement
MASK_NPCSOLID = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_MONSTERCLIP, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_MONSTER, CONTENTS_GRATE)))));
-- water physics in these contents
MASK_WATER = bit32.bor(CONTENTS_WATER, bit32.bor(CONTENTS_MOVEABLE, CONTENTS_SLIME));
-- everything that blocks lighting
MASK_OPAQUE = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, CONTENTS_OPAQUE));
-- everything that blocks lighting, but with monsters added.
MASK_OPAQUE_AND_NPCS = bit32.bor(MASK_OPAQUE, CONTENTS_MONSTER);
-- everything that blocks line of sight for AI
MASK_BLOCKLOS = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, CONTENTS_BLOCKLOS));
-- everything that blocks line of sight for AI plus NPCs
MASK_BLOCKLOS_AND_NPCS = bit32.bor(MASK_BLOCKLOS, CONTENTS_MONSTER);
-- everything that blocks line of sight for players
MASK_VISIBLE = bit32.bor(MASK_OPAQUE, CONTENTS_IGNORE_NODRAW_OPAQUE);
-- everything that blocks line of sight for players, but with monsters added.
MASK_VISIBLE_AND_NPCS = bit32.bor(MASK_OPAQUE_AND_NPCS, CONTENTS_IGNORE_NODRAW_OPAQUE);
-- bullets see these as solid
MASK_SHOT = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_MONSTER, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_DEBRIS, CONTENTS_HITBOX)))));
-- non-raycasted weapons see this as solid (includes grates)
MASK_SHOT_HULL = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_MONSTER, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_DEBRIS, CONTENTS_GRATE)))));
-- hits solids (not grates) and passes through everything else
MASK_SHOT_PORTAL = bit32.bor(CONTENTS_SOLID,  bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_WINDOW,CONTENTS_MONSTER)));
-- everything normally solid, except monsters (world+brush only)
MASK_SOLID_BRUSHONLY = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_WINDOW, CONTENTS_GRATE)));
-- everything normally solid for player movement, except monsters (world+brush only)
MASK_PLAYERSOLID_BRUSHONLY = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_PLAYERCLIP, CONTENTS_GRATE))));
-- everything normally solid for npc movement, except monsters (world+brush only)
MASK_NPCSOLID_BRUSHONLY = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_MOVEABLE, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_MONSTERCLIP, CONTENTS_GRATE))));
-- just the world, used for route rebuilding
MASK_NPCWORLDSTATIC = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_WINDOW, bit32.bor(CONTENTS_MONSTERCLIP, CONTENTS_GRATE)));
-- These are things that can split areaportals
MASK_SPLITAREAPORTAL = bit32.bor(CONTENTS_WATER, CONTENTS_SLIME);

-- UNDONE: This is untested, any moving water
MASK_CURRENT = bit32.bor(CONTENTS_CURRENT_0, bit32.bor(CONTENTS_CURRENT_90, bit32.bor(CONTENTS_CURRENT_180, bit32.bor(CONTENTS_CURRENT_270, bit32.bor(CONTENTS_CURRENT_UP, CONTENTS_CURRENT_DOWN)))));

-- everything that blocks corpse movement
-- UNDONE: Not used yet / may be deleted
MASK_DEADSOLID = bit32.bor(CONTENTS_SOLID, bit32.bor(CONTENTS_PLAYERCLIP, bit32.bor(CONTENTS_WINDOW, CONTENTS_GRATE)));
```
