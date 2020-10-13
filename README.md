# AdvancedAPI-Documentation
Documentation for nixware.cc AdvancedAPI lua

## How to use
Move AdvancedAPI.lua in directory Steam directory/steamapps/common/Counter-Strike Global Offensive/lua

## Script globals
ADVANCED_API_VERSION = 1.6; -- Current AdvancedAPI version

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

## vec3_t, vec2_t and angle_t supported operations 
- Adding '+'
- Subtraction '-'
- Multiplication '*'
- Division '/'
- Modulo '%'
- Exponentation '^'
- Unary minus '-x'
- Equivalent '=='

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

### renderer.outlined_3d_circle(origin, radius, segments, color [, percentage, walls, skip_entity, mask]) -- Drawing outlined circle 3D on origin
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
