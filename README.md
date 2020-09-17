# AdvancedAPI-Documentation
Documentation for nixware.cc AdvancedAPI lua

## How to use
Move AdvancedAPI.lua in directory Steam directory/steamapps/common/Counter-Strike Global Offensive/lua

## Script globals
ADVANCED_API_VERSION = 1.6; -- Current AdvancedAPI version

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
- m_flFlashMaxAlpha
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

struct weaponinfo_t
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
	
struct animstate_t
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
	vec3_t m_origin;
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
- math.null = 0
- math.pi_2 = 6.2831853071795862  -- PI Number, multiplicated by 2
- math.m_180_pi = 0.0174533  	  -- PI Number, divided by 180
- math.m_pi_180 = 57.2958    	  -- PI Number, multiplicated by 180
- math.int_max = 2147483647  	  -- From C/C++ library, max integer
- math.flt_epsilon = 1.192093e-07 -- Machine's zero

## vec3_t supported functions
### vec3_t:normalize() -- Normalizing vector like viewangles
```lua
local normalized = vec3_t.new(90, 181, 49):normalize(); -- Returns vec3_t object
```
### vec3_t:to_angle() -- Converts vec3_t into angle_t object
```lua
local angle = vec3_t.new(20, 40, 50):to_angle(); -- Returns angle_t object
```
### vec3_t:normalize_in_place() -- Normalizing vector
```lua
local radius = vec3_t.new(90, 181, 50):normalize_in_place(); -- Returns number
```
### vec3_t:extend(yaw, extension) -- Extends vector into yaw direction
yaw - Number, direction
extension - Number, extension amount
```lua
local extended = vec3_t.new(0, 0, 0):extend(180, 35); -- Returns vec3_t object
```
### vec3_t:dot(a) -- Calculating dot product of two vectors
```
local a = vec3_t.new(50, 50, 50);
local dot = vec3_t.new(10, 10, 10):dot(a); -- Returns number
```
### vec3_t:dist_to(a) -- Calclulating distance between two vectors`
a - vec3_t, second vector
```lua
local a = vec3_t.new(0, 0, 0);
local distance = vec3_t.new(10, 10, 10):dist_to(a); -- Returns number
```
### vec3_t:lengthsqr() -- Calculating square length of vector
```lua
local lengthsqr = vec3_t:new(10, 10, 10):lengthsqr();
```

## vec2_t supported functions
### vec2_t:normalize() -- Normalizing 2D vector
```lua
local length = vec2_t.new(10, 10):normalize(); -- Returns number
```
### vec2_t:dot(a) -- Calculating dot product of two vectors
a - vec2_t, second vector
```lua
local a = vec2_t.new(50, 50);
local dot = vec2_t.new(10, 10):dot(a); -- Returns number
```
### vec2_t:dist_to(a) -- Calclulating distance between two vectors
a - vec2_t, second vector
```lua
local a = vec2_t.new(0, 0);
local distance = vec2_t.new(10, 10):dist_to(a); -- Returns number
```
### vec2_t:lengthsqr() -- Calculating squares length
```lua
local lengthsqr = vec2_t:new(10, 10):lengthsqr(); -- Returns number
```

## angle_t supported functions
### angle_t:normalize() -- Normalizing angle like viewangles
```lua
local normalized = angle_t.new(90, 181, 49):normalize(); -- Returns angle_t object
```
### angle_t:to_vec() -- Converts angle_t into vec3_t object
```lua
local vector = angle_t.new(20, 40, 50):to_vec(); -- Returns vec3_t object
```
### angle_t:lengthsqr() -- Calculating squares length
```lua
local lengthsqr = angle_t:new(10, 10, 10):lengthsqr(); -- Returns number
```

## Math functions
### math.random_float(min, max) -- Returns random float, using vstdlib
min - Number min value
max - Number max value
```lua
local random = math.random_float(0, 10);
```

### math.round(x) -- Rounding a number
x - Number for rounding
```lua
local rounded = math.round(0.3);
```

### math.hasbit(x, p) -- Checking if number has a specific bit
x - Number
p - Sought bit
```lua
local holding_fire = math.hasbit(cmd.buttons, IN_ATTACK);
```

### math.clamp(x, min, max) -- Clamping x value
x - Number for clamping
min - Min number value
max - Max number value
```lua
local x = clamp(5, 0, 4); -- Returns number
```

### math.is_infinite(x) -- Checking if number is infinite
x - Number what we want to check
```lua
local is_infinite = math.is_infinite(math.huge);
```

### math.is_nan(x) -- Checking if number is NaN
x - Number what we want to check
```lua
local is_nan = math.is_nan(0);
```

### math.normalize_pitch(pitch) -- Normalizing pitch angle (Only for player's viewangles)
pitch - target pitch
```lua
local pitch = math.normalize_pitch(-133); -- Returns number
```

### math.normalize_yaw(yaw) -- Normalizing yaw angle (Only for player's viewangles)
yaw - target yaw
```lua
local pitch = math.normalize_pitch(722); -- Returns number
```

### math.normalize_roll(roll) -- Normalizing roll angle (Only for player's viewangles)
roll - target roll
```lua
local roll = math.normalize_roll(8); -- Returns number
```

### math.get_middle_point(a, b) -- -- Calculating middle point between two vectors
a - vec3_t, first point
b - vec3_t, second point
```lua
local middle_point = math.get_middle_point(vec3_t.new(0, 0, 0), vec3_t.new(50, 50, 50)); -- Returns vec3_t object
```

### math.calc_angle(src, dest) -- Calculating viewangles to aim at target vector
src - vec3_t, first point
dest - vec3_t, second point
```lua
local calced = math.calc_angle(engine.get_view_angles():to_vec(), vec3_t.new(50, 50, 50)); -- Returns vec3_t object
```

### math.rad2deg(x) -- Converting radians to degrees
x - Number, radians
```lua
local degrees = math.rad2deg(1.570797); -- Returns number
```

### math.deg2rad(x) -- Converting degrees to radians
x - Number, degrees
```lua
local radians = math.rad2deg(90); -- Returns number
```

### math.angle_vectors(angles) -- Converts a QAngle into or three normalised Vectors, returns table (1 - Forward, 2 - Right, 3 - Up)
angles - vec3_t, angle to convert
```lua
local directions = math.angle_vectors(engine.get_view_angles():to_vec()); -- Returns table
```

### math.vector_angles(angles) -- Converts a single Vector into a QAngle
angles - vec3_t, angle to convert
```lua
local converted = math.vector_angles(engine.get_view_angles():to_vec()); -- Returns vec3_t object
```

### math.time_to_ticks(dt) -- Converting time to ticks
dt - Number, time to convert
```lua
local ticks = math.time_to_ticks(lp:get_prop_float(m_flSimulationTime)); -- Returns number
```

### math.ticks_to_time(t) -- Converting ticks to time
t - Number, ticks to convert
```lua
local time = math.ticks_to_time(globalvars.get_tick_count()); -- Returns number
```

### math.rotate_movement(cmd, angles) -- Rotating movement into vAngles direction
cmd - usercmd_t, local commands
angles - Number, yaw direction
```lua
math.rotate_movement(cmd, 90);
```

### math.approach_angle(target, value, speed)
target - Number
value - Number
speed - Number
```lua
local unknown = math.approach_angle(13, 37, 228); -- Returns number
```

### math.angle_difference(destAngle, srcAngle) -- Getting delta between two angles
destAngle - Number, first angle
srcAngle - Number, second angle
```lua
local difference = math.angle_difference(lp:get_prop_float(m_flLowerBodyYawTarget), animstate.m_flGoalFeetYaw);
```

## FFI functions
### ffi.is_valid_ptr(p) -- Checking if pointer is valid
p - cdata/number to check
```lua
local nullptr = ffi.new('void*');
local is_valid = ffi.is_valid_ptr(nullptr);
```

### ffi.find_interface(module, interface [, print_version]) -- Finds an interface
module - String, module,where we want to search interface
interface - Interface what we want to search(Without version)
print_version - Boolean, prints interface version (optional)
```lua
local g_Prediction = ffi.find_interface("client_panorama.dll", "VClientPrediction"); -- Returns number
```

## entity_t functions
### entity_t:get_max_desync_delta() -- Calculating max desync delta of entity
```lua
local max_delta = lp:get_max_desync_delta(); -- Returns number
```

### entity_t:has_c4() -- Checking if entity has c4
```lua
local c4_carrier = lp:has_c4(); -- Returns boolean
```

### entity_t:get_active_weapon() -- Getting player's active weapon
```lua
local weapon = lp:get_active_weapon();
```

### entity_t:get_vfunc(typedef, index) -- Getting function by index from entity's vtable
```lua
local is_player_func = lp:get_vfunc("bool(__thiscall*)(void*)", 157); -- Returns function
```

### entity_t:is_weapon() -- Checking if entity is weapon
```lua
local is_weapon = lp:is_weapon(); -- Returns boolean
```

### entity_t:is_player() -- Checking if entity is player
```lua
local is_player = lp:is_player(); -- Returns boolean
```

### entity_t:get_weapon_data() -- Getting weapon data structure of weapon
```lua
local weapon_data = weapon:get_weapon_data(); -- Returns weaponinfo_t
```

### entity_t:get_animstate() -- Getting player's animstate
```lua
local animstate = lp:get_animstate(); Returns animstate_t object
```

## Weapon data functions
### entity_t:is_knife() -- Checking if weapon is knife
```lua
local is_knife = weapon:is_knife();
```

### entity_t:is_nade() -- Checking if weapon is nade
```lua
local is_nade = weapon:is_nade();
```

## Exploits
### exploits.is_recharged(local_player, weapon, exploit) -- Checking if one of exploits is recharged
local_player - entity_t, local player
weapon - entity_t, local player's weapon
exploit - number, exploit (0 - 2)
```lua
local is_recharged = exploits.is_recharged(lp, weapon, 2);
```

### exploits.get_charge(local_player, weapon, exploit) -- Calcuating exploit charge time
local_player - entity_t, local player
weapon - entity_t, local player's weapon
exploit - number, exploit (0 - 2)
```lua
local charge = exploits.get_charge(lp, weapon, 2);
```

## globalvars functions
### globalvars.get_tickrate() -- Calculating server tickrate
```lua 
local tickrate = globalvars:get_tickrate();
```

## renderer functions
### renderer.on_screen(pos2d) -- Checking if 2D vector is on screen
pos2d - vec2_t, 2d pos on screen
```lua
on_screen = renderer.on_screen(vec2_t.new(0, 0));
```

### renderer.outlined_3d_circle(origin, radius, segments, color, percentage [, walls, skip_entity, mask]) -- Drawing outlined circle 3D on origin
origin - vec3_t, origin,where we want to draw circle
radius - number, circle radius
segments - number, circle segments
color - color_t, circle color
percentage - number, circle percentage
walls - boolean, if circle should trace walls and interract with them
skip_entity - number, entity to skip in trace (walls required)
mask - number, trace mask (walls required)
```lua
renderer.outlined_3d_circle(vec3_t.new(0, 0, 0), 15, 30, color_t.new(255, 255, 255, 255), 100);
```

### renderer.box_3d(origin, width, height, color) -- Drawing 3D box on origin
origin - vec3_t, origin,where we want to draw box
width - number, box width
height - number, box height
color - color_t, circle color
```lua
renderer.box_3d(vec3_t.new(0, 0, 0), 15, 15, color_t.new(255, 255, 255, 255));
```
## Enums
### MoveType_t
```lua
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
```lua
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

### EntityFlags
```lua
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
```lua
FRAME_UNDEFINED = -1;						-- Haven't run any frames yet
FRAME_START = 0;
FRAME_NET_UPDATE_START = 1;					-- A network packet is being recieved
FRAME_NET_UPDATE_POSTDATAUPDATE_START = 2;  -- Data has been received and we're going to start calling PostDataUpdate
FRAME_NET_UPDATE_POSTDATAUPDATE_END = 3;	-- Data has been received and we've called PostDataUpdate on all data recipients
FRAME_NET_UPDATE_END = 4;					-- We've received all packets, we can now do interpolation, prediction, etc..
FRAME_RENDER_START = 5;						-- We're about to start rendering the scene
FRAME_RENDER_END = 6;						-- We've finished rendering the scene.
```

### Hitboxes
```lua
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
```lua
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
