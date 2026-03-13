local _ENV = setmetatable({}, { __index = _G })
Script = "Get Moon Stand for free at discord.gg/mfyCBWWExF"

Owner = "INTJS1"
BlackScreen = false
DisableRendering = false
FPSCap = 60
Guns = {"aug", "rifle"}
EquipGunCount = 2
DisabledGuns = {flintlock = true}
SkipAmmoFor = {["[Flintlock]"] = true}
AmmoPurchaseCount = 10
ArmorThreshold = 80
ArmorRecheckDelay = LowLagMode and 3 or 1.5
LowLagMode = true
perf = {
    loop = LowLagMode and 0.042 or 0,
    combat = LowLagMode and 0.024 or 0,
    void = LowLagMode and 0.2 or 0,
    teleport = LowLagMode and 0.024 or 0,
    teleportCombat = LowLagMode and 0.0074 or 0,
    target = LowLagMode and 0.05 or 0,
    summon = LowLagMode and 0.05 or 0,
    mask = LowLagMode and 0.1 or 0,
    equip = LowLagMode and 0.1 or 0,
    killall = LowLagMode and 0.2 or 0,
    hitbox = LowLagMode and 0.2 or 0,
    shoot = LowLagMode and 0.02 or 0,
}

local combatConfig = {
    minRange = LowLagMode and 45 or 55,
    preferredRange = LowLagMode and 92 or 108,
    maxRange = LowLagMode and 380 or 470,
    sightRangeMultiplier = 1.85,
    longRangeOrbitTrigger = 70,
    longRangeOrbitHeight = 14,
    bulletSpeed = 680,
    leadTimeMin = 0.11,
    leadTimeMax = 1.05,
    leadScale = 1.08,
    velocityBlend = 0.62,
    velocitySmoothing = 0.6,
    fastVelocitySmoothing = LowLagMode and 0.86 or 0.92,
    maxVelocitySample = LowLagMode and 620 or 760,
    fastTargetSpeedThreshold = LowLagMode and 55 or 72,
    extremeTargetSpeedThreshold = LowLagMode and 125 or 160,
    fastTargetPredictionBoost = LowLagMode and 0.64 or 0.74,
    extremeTargetPredictionBoost = LowLagMode and 0.9 or 1.02,
    fastTargetFollowSpeedBoost = LowLagMode and 2.5 or 2.74,
    extremeTargetFollowSpeedBoost = LowLagMode and 1.6 or 1.8,
    standDuelTargetSpeedThreshold = LowLagMode and 48 or 62,
    standDuelExtremeSpeedThreshold = LowLagMode and 108 or 138,
    standDuelVelocitySample = LowLagMode and 1400 or 1750,
    standDuelVelocityBlend = LowLagMode and 0.82 or 0.9,
    standDuelVelocitySmoothing = LowLagMode and 0.95 or 0.975,
    standDuelExtremeVelocitySmoothing = LowLagMode and 0.985 or 0.995,
    standDuelPredictionBoost = LowLagMode and 0.4 or 0.48,
    standDuelExtremePredictionBoost = LowLagMode and 0.6 or 0.72,
    standDuelFollowSpeedBoost = LowLagMode and 3.05 or 3.34,
    standDuelExtremeFollowSpeedBoost = LowLagMode and 1.94 or 2.12,
    standDuelSpeedCap = LowLagMode and 610 or 730,
    standDuelExtremeSpeedCap = LowLagMode and 760 or 900,
    standDuelSnapDistance = LowLagMode and 36 or 42,
    standDuelFollowMinDelay = LowLagMode and 0.00105 or 0.00088,
    standDuelLoopOrbitSpeedBoost = LowLagMode and 1.46 or 1.56,
    standDuelLoopLeadTimeBoost = LowLagMode and 0.42 or 0.52,
    standDuelLoopLeadScaleBoost = LowLagMode and 0.3 or 0.38,
    standDuelAttackLeadTimeBoost = LowLagMode and 0.16 or 0.22,
    standDuelAttackLeadScaleBoost = LowLagMode and 0.12 or 0.16,
    attackPreferredRange = LowLagMode and 98 or 118,
    attackMaxRange = LowLagMode and 460 or 580,
    attackShootRange = LowLagMode and 3400 or 4600,
    attackBlindShootRange = LowLagMode and 4600 or 6200,
    attackSightRangeMultiplier = LowLagMode and 6.8 or 8.2,
    attackShootInterval = LowLagMode and 0.0036 or 0.0025,
    attackMinShootInterval = LowLagMode and 0.0026 or 0.0019,
    attackShotsPerTick = LowLagMode and 8 or 9,
    attackLeadTimeMax = LowLagMode and 1.5 or 1.85,
    attackLeadScale = LowLagMode and 1.96 or 2.3,
    attackPredictionBoost = LowLagMode and 0.24 or 0.3,
    attackFollowSpeedBoost = LowLagMode and 1.72 or 1.86,
    attackExtremeFollowSpeedBoost = LowLagMode and 1.48 or 1.6,
    attackCircleRadius = LowLagMode and 9.8 or 11.6,
    attackCircleStrafeSpeed = LowLagMode and 560 or 650,
    attackCircleHeight = LowLagMode and 4.4 or 5.0,
    attackCircleHeightBob = LowLagMode and 0.08 or 0.14,
    attackFollowMinDelay = LowLagMode and 0.0016 or 0.00135,
    -- .l / .lk long-range dominance profile.
    loopShootRange = LowLagMode and 16500 or 22000,
    loopBlindShootRange = LowLagMode and 24000 or 30000,
    loopSightRangeMultiplier = LowLagMode and 10.2 or 12.0,
    loopShootInterval = LowLagMode and 0.0039 or 0.0028,
    loopMinShootInterval = LowLagMode and 0.0027 or 0.0019,
    loopShotsPerTick = LowLagMode and 9 or 10,
    loopLeadTimeMax = LowLagMode and 6.2 or 6.8,
    loopLeadScale = LowLagMode and 3.32 or 3.92,
    loopMinRange = LowLagMode and 240 or 280,
    loopPreferredRange = LowLagMode and 380 or 450,
    loopMaxRange = LowLagMode and 640 or 760,
    loopFollowMinDelay = LowLagMode and 0.0012 or 0.00098,
    indoorLoopSpeedBoost = LowLagMode and 1.6 or 1.76,
    indoorLoopRadiusScale = LowLagMode and 0.92 or 0.98,
    indoorLoopEvasionRadius = LowLagMode and 1.8 or 2.2,
    indoorLoopBaseHeight = LowLagMode and 5.2 or 6.2,
    indoorLoopHeightBob = LowLagMode and 0.75 or 1.0,
    loopSkyStrafeSpeed = LowLagMode and 700 or 790,
    loopSkyStrafeRadiusPull = LowLagMode and 0.22 or 0.26,
    loopSkyStrafeHeightBob = LowLagMode and 1.0 or 1.4,
    indoorCircleRadius = LowLagMode and 13.5 or 15.5,
    indoorCircleStrafeSpeed = LowLagMode and 340 or 420,
    indoorCircleHeight = LowLagMode and 4.6 or 5.3,
    sentryCircleRadius = LowLagMode and 9.4 or 11.2,
    sentryCircleStrafeSpeed = LowLagMode and 520 or 610,
    sentryCircleHeight = LowLagMode and 4.2 or 5.0,
    sentryCircleHeightBob = LowLagMode and 0.16 or 0.24,
    sentryShootInterval = LowLagMode and 0.0044 or 0.003,
    sentryMinShootInterval = LowLagMode and 0.003 or 0.0022,
    sentryShotsPerTick = LowLagMode and 8 or 9,
    sentryFollowMinDelay = LowLagMode and 0.00128 or 0.00105,

    -- Indoor (building) handling: orbit aggressively + boost fire rate.
    indoorCheckInterval = 0.1,
    indoorRoofCheckDistance = 45,
    indoorRoofMaxDistance = 22,
    indoorWallCheckDistance = 12,
    indoorWallHitThreshold = 2,
    indoorOrbitRadius = LowLagMode and 11 or 13,
    -- Keep the stand elevated during loops; prevents the orbit from dragging on the ground.
    loopOrbitMinHeight = LowLagMode and 10 or 12,
    -- Force sky combat height so the stand shoots from above.
    skyCombatMinHeight = LowLagMode and 60 or 80,
    skyCombatMinAbsY = LowLagMode and 60 or 80,
    -- Outdoor loop orbit (for .l / .lk): fast fly-like circle around target.
    loopOrbitRadius = LowLagMode and 62 or 74,
    loopOrbitSpeed = LowLagMode and 208 or 232, -- radians/sec
    indoorOrbitHeight = LowLagMode and 10 or 12,
    indoorOrbitCeilingMargin = 1.5,
    indoorOrbitSpeed = LowLagMode and 180 or 202, -- radians/sec
    -- Keep a small non-zero interval so remotes do not flood every Heartbeat.
    indoorShootInterval = LowLagMode and 0.0082 or 0.0062,
    indoorShotsPerTick = LowLagMode and 20 or 24,
}

defaultPerf = {}
for k, v in pairs(perf) do
    defaultPerf[k] = v
end
defaultCombatConfig = {}
for k, v in pairs(combatConfig) do
    defaultCombatConfig[k] = v
end
defaultConfig = {}
defaultConfigCaptured = false

function standWait(base)
    if stand2Active then
        return math.min(base, 0.015)
    end
    return base
end

local function clamp(value, minValue, maxValue)
    if value < minValue then
        return minValue
    elseif value > maxValue then
        return maxValue
    end
    return value
end

followState = {
    lastTargetPosition = nil,
    targetVelocity = Vector3.new(),
    lastUpdate = os.clock(),
    currentTargetId = nil,
    currentTargetCharacter = nil,
    lastTargetWasKO = nil,
    lastTargetWasDead = nil,
    standDuelTarget = false,
    standDuelExtreme = false,
}

standTuning = {
    movementScale = 1.78,
    loopOrbitScale = 1.98,
    indoorOrbitScale = 2.04,
    maxBurstShots = 13,
    minShootInterval = 0.0068,
    minFollowShotCooldown = 0.022,
    minTeleportDelay = 0.00062,
}

networkTuning = {
    shotPressureDecay = 0.28,
    shotPressureSoft = 52,
    shotPressureHard = 94,
    minBurstScale = 0.38,
    followMinBurstScale = 0.36,
    minFollowTargetScale = 0.48,
}

movementTuning = {
    pressureDecay = 0.22,
    pressureSoft = 110,
    pressureHard = 185,
    minDelayScale = 1.45,
    hardDelayScale = 2.1,
}

shotPressure = 0
lastShotPressureUpdate = os.clock()
movementPressure = 0
lastMovementPressureUpdate = os.clock()

function getShotPressure()
    local now = os.clock()
    local dt = now - (lastShotPressureUpdate or now)
    if dt > 0 then
        shotPressure = shotPressure * math.exp(-dt / (networkTuning.shotPressureDecay or 0.35))
        lastShotPressureUpdate = now
    end
    return shotPressure
end

function addShotPressure(amount)
    shotPressure = getShotPressure() + math.max(amount or 0, 0)
    return shotPressure
end

function getNetworkBurstScale(followMode)
    local pressure = getShotPressure()
    local soft = networkTuning.shotPressureSoft or 60
    local hard = networkTuning.shotPressureHard or (soft + 50)
    local minScale = followMode and (networkTuning.followMinBurstScale or 0.4) or (networkTuning.minBurstScale or 0.45)
    if pressure <= soft then
        return 1
    end
    if pressure >= hard then
        return minScale
    end
    local alpha = (pressure - soft) / math.max(hard - soft, 1)
    return 1 - (alpha * (1 - minScale))
end

function getMovementPressure()
    local now = os.clock()
    local dt = now - (lastMovementPressureUpdate or now)
    if dt > 0 then
        movementPressure = movementPressure * math.exp(-dt / (movementTuning.pressureDecay or 0.22))
        lastMovementPressureUpdate = now
    end
    return movementPressure
end

function addMovementPressure(amount)
    movementPressure = getMovementPressure() + math.max(amount or 0, 0)
    return movementPressure
end

function getMovementDelayScale()
    local pressure = getMovementPressure()
    local soft = movementTuning.pressureSoft or 110
    local hard = movementTuning.pressureHard or (soft + 75)
    local minScale = movementTuning.minDelayScale or 1.45
    local hardScale = movementTuning.hardDelayScale or 2.1
    if pressure <= soft then
        return 1
    end
    if pressure >= hard then
        return hardScale
    end
    local alpha = (pressure - soft) / math.max(hard - soft, 1)
    return minScale + ((hardScale - minScale) * alpha)
end

function resetFollowPrediction()
    followState.lastTargetPosition = nil
    followState.targetVelocity = Vector3.zero
    followState.lastUpdate = os.clock()
    followState.standDuelTarget = false
    followState.standDuelExtreme = false
end

function resetCombatFireWindow()
    followFireInProgress = false
    lastShootAt = 0
    lastFollowShotAt = 0
    lastFlameActivateAt = 0
end

lastCombatShotSuccessAt = 0
lastRespawnCombatBootstrapAt = 0
lastCombatRecoveryWatchdogAt = 0

if not game:IsLoaded() then game.Loaded:Wait() end

player = game.Players.LocalPlayer

Players = game:GetService("Players")
LocalPlayer = Players.LocalPlayer
UserInputService = game:GetService("UserInputService")

Bots = {}

Bots[LocalPlayer.Name] = LocalPlayer.Name

Player = Players.LocalPlayer
Character = Player.Character or Player.CharacterAdded:Wait()
currentGunIndex = 1

gunData = {
    rifle = {
        toolName = "[Rifle]",
        shopName = "[Rifle] - $1694"
    },
    aug = {
        toolName = "[AUG]",
        shopName = "[AUG] - $2131"
    },
    flintlock = {
        toolName = "[Flintlock]",
        shopName = "[Flintlock] - $1421"
    },
    lmg = {
        toolName = "[LMG]",
        shopName = "[LMG] - $4098"
    },
    db = {
        toolName = "[Double-Barrel SG]",
        shopName = "[Double-Barrel SG] - $1475"
    },
    flamethrower = {
        toolName = "[Flamethrower]",
        shopName = "[Flamethrower] - $10130"
    },
}

-- Shared destination map for .to / .goto / deliveries.
locationCFrames = {
    rifle = CFrame.new(-265, 52, -220),
    armor = CFrame.new(-933, -25, 570),
    armmor = CFrame.new(-933, -25, 570),
    armour = CFrame.new(-933, -25, 570),
    lmg = CFrame.new(-618, 23, -299),
    mil = CFrame.new(36, 50, -830),
    military = CFrame.new(36, 50, -830),
    rev = CFrame.new(-639, 21, -125),
    revolver = CFrame.new(-639, 21, -125),
    food = CFrame.new(-327, 23, -291),
    food2 = CFrame.new(305, 49, -622),
    roof = CFrame.new(-326, 80, -293),
    bank = CFrame.new(-467, 39, -284),
    school = CFrame.new(-587, 68, 330),
    rpg = CFrame.new(113, -27, -268),
    uphill = CFrame.new(503, 48, -591),
    downhill = CFrame.new(-563, 8, -716),
    gs = CFrame.new(415.067, 76.778, 1.685),
}

-- BrownBag shop fallback pivot from map inspector (used by .bag command).
brownBagShopFallbackCFrame = CFrame.new(-316.034, 48.279, -723.86)
brownBagActionInProgress = false
brownBagTargetName = nil
-- Flamethrower shop/ammo fallback pivots from map inspector (used by .f command).
flameShopFallbackCFrame = CFrame.new(-157.122, 50.913, -105.401)
flameAmmoFallbackCFrame = CFrame.new(-150.322, 50.909, -105.801)
FLAME_TOOL_NAME = "[Flamethrower]"
FLAME_SHOP_NAME = "[Flamethrower] - $10130"
FLAME_AMMO_ITEM_NAME = "140 [Flamethrower Ammo] - $1126"

RunService = game:GetService("RunService")

if DisableRendering then
    RunService:Set3dRenderingEnabled(false)
end

Lighting = game:GetService("Lighting")

Lighting.GlobalShadows = false

for _, obj in pairs(workspace:GetDescendants()) do
    if obj:IsA("ParticleEmitter") or obj:IsA("Trail") then
        obj.Enabled = false
    end
end

workspace.StreamingEnabled = true

getgenv().enabled = false
getgenv().enabled1 = false
auraspeed = 11
auradistance = 4
auraangle = math.random() * math.pi * 2
homeFollowDistance = 4.6
homeFollowSideOffset = 2.2
homeFollowHeight = 1.18
homeFollowPredictionTime = 0.125
homeFollowCatchup = 0.88
homeFollowSnapDistance = 38
homeFollowFarSnapDistance = 88
homeFollowMotionSpeed = 7.0
homeFollowSideWave = 0.78
homeFollowBob = 0.1
homeFollowMaxDistanceBoost = 3.8
homeFollowLookHeight = 1.42
voidAuraSpeed = 28
voidAuraRadius = 130
voidAuraRadiusJitter = 30
voidAuraVerticalBob = 10
voidAuraCenterDrift = 20
voidAuraRecenterSeconds = 7
defaultTeleportRange = 20
loopTeleportRange = 45
standHomeName = Owner
stand2Active = false
stand2TargetName = nil
stand2TargetUserId = nil
stand2CurrentTarget = nil
powerModeActive = false
standPerformanceModeActive = false
buyingArmorInProgress = false
autoArmorEnabled = true
autoFireArmorEnabled = false -- Don't auto-buy fire armor.
lastArmorPurchase = 0
postResetCombatRecoveryActive = false
postResetCombatRecoveryUntil = 0

lockedTarget = nil
grabCheckEnabled = true
koCheckEnabled = true
buyingInProgress = false
buyingGunInProgress = false
buyingMaskInProgress = false
buyingVehicleInProgress = false
immediateLoadoutPrimeInProgress = false
combatLoadoutDemandUntil = 0
lastImmediateLoadoutPrimeRequestAt = 0
AbuseProtection = false
teleporting = false
autodrop = false
ragebottargets = {}
currentTargetIndex = 1
fakepositionconnection = nil

-- Global hard stop latch (set by .v). When true, combat/movement logic should not run.
hardStop = false

-- Loop targeting support for .l / .lk
shouldSwitch = false
function isValidLoopTarget(plr)
    if not plr or not plr:IsDescendantOf(game) then
        return false
    end
    local char = plr.Character
    if not char then
        return false
    end
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hum or hum.Health <= 0 then
        return false
    end
    local body = char:FindFirstChild("BodyEffects")
    if body then
        local sDeath = body:FindFirstChild("SDeath")
        if sDeath and sDeath.Value then
            return false
        end
    end
    return true
end
automaskenabled = false
trashtalkactive = false
fpactive = false
refreshingfakeposition = false
didRefreshOnDeath = false
autoSaveEnabled = false
autoSavePosition = Vector3.new(-490.6, 93.412, -91.7)
autosaveActive = false
toDeliveryActive = false
toDeliveryRunId = 0
lastToDestination = nil
lastToDropCFrame = nil
flameModeActive = false
flameModeTargetUserId = nil
flameModeTargetName = nil
smiteCommandInProgress = false
smiteRunId = 0
standCommandBusyUntil = 0
manualVoidHold = false
lastCarryCombatRecoveryAt = 0
lastCarryReleaseFlushAt = 0

function markStandCommandBusy(duration)
    local holdSeconds = tonumber(duration) or 3.5
    local expireAt = os.clock() + math.max(0.35, holdSeconds)
    if expireAt > (standCommandBusyUntil or 0) then
        standCommandBusyUntil = expireAt
    end
end

function isStandCommandBusy()
    return (standCommandBusyUntil or 0) > os.clock()
end

function clearStandCommandBusy()
    standCommandBusyUntil = 0
end

function activateManualVoidHold()
    manualVoidHold = true
end

function clearManualVoidHold()
    manualVoidHold = false
end

function isManualVoidHoldActive()
    return manualVoidHold == true
end
smiteTargetUserId = nil
smiteTargetName = nil
SMITE_MAX_ATTEMPTS = 2
SMITE_ATTEMPT_DURATION = 8
SMITE_OUT_OF_MAP_XZ = 2200
SMITE_OUT_OF_MAP_MIN_Y = -180
SMITE_OUT_OF_MAP_MAX_Y = 2500
SMITE_TRACK_INTERVAL = 0.016
SMITE_TOUCH_RADIUS = 1.2
SMITE_PREDICT_TIME = 0.095

function cancelSmiteCommandState()
    smiteCommandInProgress = false
    smiteTargetUserId = nil
    smiteTargetName = nil
    smiteRunId += 1
end

Players = game:GetService("Players")
RunService = game:GetService("RunService")
player = game.Players.LocalPlayer
character = game.Players.LocalPlayer.Character
LocalPlayer = Players.LocalPlayer
ReplicatedStorage = game:GetService('ReplicatedStorage')
Workspace = game:GetService("Workspace")
camera = workspace.CurrentCamera
_, y, r = camera.CFrame:ToOrientation()

-- Avoid infinite yield warnings from missing objects in some games.
function ensureChild(parent, className, name)
    local child = parent:FindFirstChild(name)
    if child then
        return child
    end
    local inst = Instance.new(className)
    inst.Name = name
    inst.Parent = parent
    return inst
end

ensureChild(ReplicatedStorage, "RemoteEvent", "FW_ShowEvent")

function ensureLeaderstats(plr)
    if not plr:FindFirstChild("leaderstats") then
        local stats = Instance.new("Folder")
        stats.Name = "leaderstats"
        stats.Parent = plr
    end
end

for _, plr in ipairs(Players:GetPlayers()) do
    ensureLeaderstats(plr)
end

Players.PlayerAdded:Connect(ensureLeaderstats)

getgenv().whitelist = {}
getgenv().sentryprotected = {}
getgenv().sentryprotectedUsers = {}
getgenv().sentrywhitelisted = {}
getgenv().protectedwhitelist = {}

getgenv().protectedwhitelist[Owner] = true

basePosition = Vector3.new(87240, 29628, -482290)

whitelistZone = Instance.new("Part")
whitelistZone.Name = "WhitelistBeacon"
whitelistZone.Anchored = true
whitelistZone.CanCollide = true
whitelistZone.Transparency = 1
whitelistZone.Size = Vector3.new(30, 10, 30)
whitelistZone.Position = basePosition
whitelistZone.Parent = workspace

wallFront = Instance.new("Part")
wallFront.Name = "WhitelistBeacon_WallFront"
wallFront.Anchored = true
wallFront.CanCollide = true
wallFront.Transparency = 1
wallFront.Size = Vector3.new(32, 10, 1)
wallFront.Position = basePosition + Vector3.new(0, 5, 15.5)
wallFront.Parent = workspace

wallBack = Instance.new("Part")
wallBack.Name = "WhitelistBeacon_WallBack"
wallBack.Anchored = true
wallBack.CanCollide = true
wallBack.Transparency = 1
wallBack.Size = Vector3.new(32, 10, 1)
wallBack.Position = basePosition + Vector3.new(0, 5, -15.5)
wallBack.Parent = workspace

wallLeft = Instance.new("Part")
wallLeft.Name = "WhitelistBeacon_WallLeft"
wallLeft.Anchored = true
wallLeft.CanCollide = true
wallLeft.Transparency = 1
wallLeft.Size = Vector3.new(1, 10, 30)
wallLeft.Position = basePosition + Vector3.new(-15.5, 5, 0)
wallLeft.Parent = workspace

wallRight = Instance.new("Part")
wallRight.Name = "WhitelistBeacon_WallRight"
wallRight.Anchored = true
wallRight.CanCollide = true
wallRight.Transparency = 1
wallRight.Size = Vector3.new(1, 10, 30)
wallRight.Position = basePosition + Vector3.new(15.5, 5, 0)
wallRight.Parent = workspace

roof = Instance.new("Part")
roof.Name = "WhitelistBeacon_Roof"
roof.Anchored = true
roof.CanCollide = true
roof.Transparency = 1
roof.Size = Vector3.new(32, 1, 32)
roof.Position = basePosition + Vector3.new(0, 10.5, 0)
roof.Parent = workspace

Players = game:GetService("Players")
LocalPlayer = Players.LocalPlayer

zoneSize = Vector3.new(20, 10, 20)
basePosition = whitelistZone.Position
WHITELIST_RADIUS = 20

function getRandomPositionInZone()
    local halfSize = zoneSize / 2
    local randomX = basePosition.X + math.random() * zoneSize.X - halfSize.X
    local randomZ = basePosition.Z + math.random() * zoneSize.Z - halfSize.Z
    local fixedY = basePosition.Y + halfSize.Y + 3
    return Vector3.new(randomX, fixedY, randomZ)
end

function teleportPlayerRandomly()
    local character = LocalPlayer.Character
    if not character then return end
    local hrp = character:FindFirstChild("HumanoidRootPart")
    if not hrp then return end

    hrp.Velocity = Vector3.zero
    hrp.RotVelocity = Vector3.zero
    hrp.AssemblyLinearVelocity = Vector3.zero
    hrp.AssemblyAngularVelocity = Vector3.zero

    local randomPos = getRandomPositionInZone()
    hrp.CFrame = CFrame.new(randomPos)

    hrp.Velocity = Vector3.zero
    hrp.RotVelocity = Vector3.zero
    hrp.AssemblyLinearVelocity = Vector3.zero
    hrp.AssemblyAngularVelocity = Vector3.zero
end

function isPlayerNearPosition(player, position, radius)
    local char = player.Character
    if not char then return false end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return false end

    local distance = (hrp.Position - position).Magnitude
    return distance <= radius
end

function checkWhitelistNearPosition()
    for _, player in pairs(Players:GetPlayers()) do
        if isPlayerNearPosition(player, basePosition, WHITELIST_RADIUS) then
            if not getgenv().whitelist[player.Name] then
                getgenv().whitelist[player.Name] = true
            end
        end
    end
end

function findPlayerByPartial(input)
    if not input then
        return nil
    end
    input = input:lower()
    for _, plr in ipairs(Players:GetPlayers()) do
        local name = plr.Name:lower()
        local display = plr.DisplayName:lower()
        if name:find(input, 1, true) or display:find(input, 1, true) then
            return plr
        end
    end
    return nil
end

local function resolveDeliveryTargetPlayer(rawInput)
    if not rawInput then
        return nil
    end
    local input = tostring(rawInput):lower()
    if input == "" then
        return nil
    end

    local bestPrefix = nil
    local bestContains = nil
    local bestPrefixScore = math.huge
    local bestContainsScore = math.huge

    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Name ~= Owner then
            local name = plr.Name:lower()
            local display = plr.DisplayName:lower()

            -- Prefer exact matches first for reliability.
            if name == input or display == input then
                return plr
            end

            local prefixMatch = name:sub(1, #input) == input or display:sub(1, #input) == input
            if prefixMatch then
                local score = math.min(#name, #display)
                if score < bestPrefixScore then
                    bestPrefixScore = score
                    bestPrefix = plr
                end
            else
                local containsMatch = name:find(input, 1, true) or display:find(input, 1, true)
                if containsMatch then
                    local score = math.min(#name, #display)
                    if score < bestContainsScore then
                        bestContainsScore = score
                        bestContains = plr
                    end
                end
            end
        end
    end

    return bestPrefix or bestContains
end

function getPlayerCrew(player)
    if not player then return nil end
    local dataFolder = player:FindFirstChild("DataFolder")
    if not dataFolder then return nil end
    local information = dataFolder:FindFirstChild("Information")
    if not information then return nil end
    local crew = information:FindFirstChild("Crew")
    if not crew then return nil end
    return tostring(crew.Value)
end

function isInSameCrew(player1, player2)
    if not player1 or not player2 then return false end
    local crew1 = getPlayerCrew(player1)
    local crew2 = getPlayerCrew(player2)
    if not crew1 or not crew2 then return false end
    return crew1 == crew2 and crew1 ~= "None" and crew1 ~= ""
end

function trimInput(input)
    if not input then
        return nil
    end
    return input:gsub("^%s+", ""):gsub("%s+$", "")
end

handleStand2Command = nil
disableStand2 = nil
activatePowerMode = nil
deactivatePowerMode = nil
activateStandPerformanceMode = nil
deactivateStandPerformanceMode = nil

targetPlayer = nil
lastOwnerPosition = nil
shootRunning = true
shotsPerTick = LowLagMode and 3 or 6
followShotsPerTick = LowLagMode and 1 or 2
followShotCooldown = LowLagMode and 0.08 or 0.04
followGunSpacing = 0.01
followGridCellSize = 8
followGridRadius = LowLagMode and 170 or 220
followMaxTargets = LowLagMode and 8 or 12
followShootThroughWalls = true
ownerFollowShotsPerTick = LowLagMode and 2 or 3
ownerFollowShotCooldown = LowLagMode and 0.045 or 0.025
ownerFollowGunSpacing = LowLagMode and 0.006 or 0.004
ownerFollowReloadCooldown = LowLagMode and 0.24 or 0.18
lastFollowShotAt = 0
followFireInProgress = false
shootInterval = perf.shoot
lastShootAt = 0
lastFlameActivateAt = 0
combatPrimeWindowUntil = 0
lastCombatPrimeRefreshAt = 0
lastCombatPrimeTargetUserId = nil
FLAME_HOLD_CLICK_INTERVAL = 0.10
lastFlameStompAt = 0
FLAME_ORBIT_RADIUS = 7.5
FLAME_ORBIT_HEIGHT = 0.25
FLAME_ORBIT_SPEED = 8.8
function getShootHandle(tool)
    if not tool or not tool:IsA("Tool") then return nil end
    local toolName = tostring(tool.Name or "")
    local isFlameTool = (toolName == FLAME_TOOL_NAME) or toolName:lower():find("flamethrower", 1, true)
    if (not isFlameTool) and (not tool:FindFirstChild("Ammo")) then
        return nil
    end
    local handle = tool:FindFirstChild("Handle")
    if not handle or not handle.Parent then return nil end
    return handle
end
function isGunTool(tool)
    if not (tool and tool:IsA("Tool")) then
        return false
    end
    local toolName = tostring(tool.Name or "")
    if toolName == FLAME_TOOL_NAME or toolName:lower():find("flamethrower", 1, true) then
        return tool:FindFirstChild("Handle") ~= nil
    end
    return tool:FindFirstChild("Ammo") ~= nil
end
function getGunToolByKey(gunKey)
    local info = gunData[gunKey]
    if not info then
        return nil
    end
    local toolName = info.toolName
    local lp = game.Players.LocalPlayer
    local char = lp and lp.Character
    if char then
        local tool = char:FindFirstChild(toolName)
        if tool and tool:IsA("Tool") then
            return tool
        end
    end
    local backpack = lp and lp:FindFirstChild("Backpack")
    if backpack then
        local tool = backpack:FindFirstChild(toolName)
        if tool and tool:IsA("Tool") then
            return tool
        end
    end
    return nil
end
function collectGunTools()
    local tools = {}
    local seen = {}
    local lp = game.Players.LocalPlayer

    local function addTool(tool)
        if tool and not seen[tool] and getShootHandle(tool) then
            seen[tool] = true
            table.insert(tools, tool)
        end
    end

    local char = lp and lp.Character
    if char then
        for _, child in ipairs(char:GetChildren()) do
            addTool(child)
        end
    end

    local backpack = lp and lp:FindFirstChild("Backpack")
    if backpack then
        for _, child in ipairs(backpack:GetChildren()) do
            addTool(child)
        end
    end

    return tools
end
function isAliveCharacter(char)
    if not char then
        return false
    end
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    if not humanoid or humanoid.Health <= 0 then
        return false
    end
    local bodyEffects = char:FindFirstChild("BodyEffects")
    if bodyEffects then
        local koValue = bodyEffects:FindFirstChild("K.O")
        if koValue and koValue.Value then
            return false
        end
        local sDeathValue = bodyEffects:FindFirstChild("SDeath")
        if sDeathValue and sDeathValue.Value then
            return false
        end
    end
    return true
end
function collectGridTargets(centerPos)
    local lp = game.Players.LocalPlayer
    local cells = {}
    if not centerPos or followGridCellSize <= 0 or followGridRadius <= 0 then
        return {}
    end
    for _, player in ipairs(game.Players:GetPlayers()) do
        local char = player.Character
        if player ~= lp and player ~= targetPlayer
            and not getgenv().whitelist[player.Name]
            and not getgenv().protectedwhitelist[player.Name]
            and not isInSameCrew(lp, player)
            and char and char:FindFirstChild("Head")
            and not char:FindFirstChild("GRABBING_CONSTRAINT")
            and not char:FindFirstChild("ForceField")
            and isAliveCharacter(char) then
            local head = char.Head
            local offset = head.Position - centerPos
            if offset.Magnitude <= followGridRadius then
                local gx = math.floor(offset.X / followGridCellSize)
                local gz = math.floor(offset.Z / followGridCellSize)
                local key = gx .. ":" .. gz
                local cellCenter = Vector3.new(
                    centerPos.X + (gx + 0.5) * followGridCellSize,
                    head.Position.Y,
                    centerPos.Z + (gz + 0.5) * followGridCellSize
                )
                local score = (head.Position - cellCenter).Magnitude
                local entry = cells[key]
                if not entry or score < entry.score then
                    cells[key] = {gx = gx, gz = gz, player = player, score = score}
                end
            end
        end
    end
    local list = {}
    for _, entry in pairs(cells) do
        table.insert(list, entry)
    end
    table.sort(list, function(a, b)
        local da = math.abs(a.gx) + math.abs(a.gz)
        local db = math.abs(b.gx) + math.abs(b.gz)
        if da == db then
            if a.gz == b.gz then
                return a.gx < b.gx
            end
            return a.gz < b.gz
        end
        return da < db
    end)
    local targets = {}
    local limit = math.min(#list, followMaxTargets)
    for i = 1, limit do
        table.insert(targets, list[i].player)
    end
    return targets
end
reloadCooldown = 0.4
lastReloadAt = {}

function captureDefaultConfig()
    if defaultConfigCaptured then
        return
    end
    defaultConfig = {
        LowLagMode = LowLagMode,
        auraspeed = auraspeed,
        auradistance = auradistance,
        homeFollowDistance = homeFollowDistance,
        homeFollowSideOffset = homeFollowSideOffset,
        homeFollowHeight = homeFollowHeight,
        homeFollowPredictionTime = homeFollowPredictionTime,
        homeFollowCatchup = homeFollowCatchup,
        homeFollowSnapDistance = homeFollowSnapDistance,
        homeFollowFarSnapDistance = homeFollowFarSnapDistance,
        homeFollowMotionSpeed = homeFollowMotionSpeed,
        homeFollowSideWave = homeFollowSideWave,
        homeFollowBob = homeFollowBob,
        homeFollowMaxDistanceBoost = homeFollowMaxDistanceBoost,
        homeFollowLookHeight = homeFollowLookHeight,
        shotsPerTick = shotsPerTick,
        followShotsPerTick = followShotsPerTick,
        followShotCooldown = followShotCooldown,
        followGunSpacing = followGunSpacing,
        followGridCellSize = followGridCellSize,
        followGridRadius = followGridRadius,
        followMaxTargets = followMaxTargets,
        reloadCooldown = reloadCooldown,
        hitboxsize = hitboxsize,
        FPSCap = FPSCap,
        ArmorRecheckDelay = ArmorRecheckDelay,
    }
    defaultConfigCaptured = true
end

local DEFAULT_CONFIG_KEYS = {
    "auraspeed",
    "auradistance",
    "homeFollowDistance",
    "homeFollowSideOffset",
    "homeFollowHeight",
    "homeFollowPredictionTime",
    "homeFollowCatchup",
    "homeFollowSnapDistance",
    "homeFollowFarSnapDistance",
    "homeFollowMotionSpeed",
    "homeFollowSideWave",
    "homeFollowBob",
    "homeFollowMaxDistanceBoost",
    "homeFollowLookHeight",
    "shotsPerTick",
    "followShotsPerTick",
    "followShotCooldown",
    "followGunSpacing",
    "followGridCellSize",
    "followGridRadius",
    "followMaxTargets",
    "reloadCooldown",
    "hitboxsize",
    "FPSCap",
    "ArmorRecheckDelay",
}

local function applyDefaultScalarConfig()
    for _, key in ipairs(DEFAULT_CONFIG_KEYS) do
        local value = defaultConfig[key]
        if value ~= nil then
            _G[key] = value
        end
    end

    auraspeed = defaultConfig.auraspeed
    auradistance = defaultConfig.auradistance
    homeFollowDistance = defaultConfig.homeFollowDistance
    homeFollowSideOffset = defaultConfig.homeFollowSideOffset
    homeFollowHeight = defaultConfig.homeFollowHeight
    homeFollowPredictionTime = defaultConfig.homeFollowPredictionTime
    homeFollowCatchup = defaultConfig.homeFollowCatchup
    homeFollowSnapDistance = defaultConfig.homeFollowSnapDistance
    homeFollowFarSnapDistance = defaultConfig.homeFollowFarSnapDistance
    homeFollowMotionSpeed = defaultConfig.homeFollowMotionSpeed
    homeFollowSideWave = defaultConfig.homeFollowSideWave
    homeFollowBob = defaultConfig.homeFollowBob
    homeFollowMaxDistanceBoost = defaultConfig.homeFollowMaxDistanceBoost
    homeFollowLookHeight = defaultConfig.homeFollowLookHeight
    shotsPerTick = defaultConfig.shotsPerTick
    followShotsPerTick = defaultConfig.followShotsPerTick
    followShotCooldown = defaultConfig.followShotCooldown
    followGunSpacing = defaultConfig.followGunSpacing
    followGridCellSize = defaultConfig.followGridCellSize
    followGridRadius = defaultConfig.followGridRadius
    followMaxTargets = defaultConfig.followMaxTargets
    reloadCooldown = defaultConfig.reloadCooldown
    hitboxsize = defaultConfig.hitboxsize
    FPSCap = defaultConfig.FPSCap
    ArmorRecheckDelay = defaultConfig.ArmorRecheckDelay
end

local function restoreDefaultCombatConfig()
    for k, v in pairs(defaultCombatConfig) do
        combatConfig[k] = v
    end
end

function isReloading()
    local lp = game.Players.LocalPlayer
    local char = lp and lp.Character
    local bodyEffects = char and char:FindFirstChild("BodyEffects")
    local reloadFlag = bodyEffects and bodyEffects:FindFirstChild("Reload")
    return reloadFlag and reloadFlag.Value
end

function tryReloadTool(tool)
    local ammo = tool and tool:FindFirstChild("Ammo")
    if not ammo or ammo.Value > 0 then
        return false
    end
    if isReloading() then
        return true
    end
    local now = os.clock()
    if lastReloadAt[tool] and (now - lastReloadAt[tool]) < reloadCooldown then
        return true
    end
    lastReloadAt[tool] = now
    ReplicatedStorage.MainEvent:FireServer("Reload", tool)
    return true
end
function fireToolAtTarget(tool, targetPart, shots, aimPosition)
    local lp = game.Players.LocalPlayer
    local char = lp and lp.Character
    if not (tool and char and targetPart) then
        return
    end
    local equippedNow = false
    if tool.Parent ~= char then
        tool.Parent = char
        equippedNow = true
    end
    if equippedNow then
        RunService.Heartbeat:Wait()
        if tool.Parent ~= char then
            return
        end
    end
    local handle = getShootHandle(tool)
    if not handle then
        return
    end
    shots = shots or 1
    if tryReloadTool(tool) then
        return
    end
    shots = math.max(1, math.floor(shots + 0.5))
    local origin = handle.Position
    if followShootThroughWalls and targetPart then
        local delta = targetPart.Position - origin
        if delta.Magnitude > 0 then
            origin = origin + delta.Unit * 0.1
        end
    end
    local targetAim = aimPosition or targetPart.Position
    addShotPressure(shots)
    lastCombatShotSuccessAt = os.clock()
    for _ = 1, shots do
        ReplicatedStorage.MainEvent:FireServer(
            "ShootGun",
            handle,
            origin,
            targetAim,
            targetPart,
            Vector3.new(0, 0, 0)
        )
    end
end

local function getPowerModeShotBudget(distance, loopModeActive, directAttackMode, sentryModeActive, targetIndoors, standDuelTarget, standDuelExtreme)
    local totalBudget
    if loopModeActive then
        totalBudget = targetIndoors and 12 or 10
    elseif directAttackMode then
        totalBudget = 9
    elseif sentryModeActive then
        totalBudget = 8
    else
        totalBudget = 7
    end

    if distance >= 140 then
        totalBudget -= 1
    end
    if distance >= 260 then
        totalBudget -= 1
    end
    if standDuelTarget then
        totalBudget += 1
    end
    if standDuelExtreme then
        totalBudget += 1
    end

    return clamp(totalBudget, 4, targetIndoors and 12 or 10)
end

noclipActive = false
standGhostActive = false
standPartDefaults = {}
standGhostPanicSeconds = 3.2
standEvasionSeconds = 2.8
standLastHitAt = -1e9
standHealthConn = nil
standDefenseMode = true
standMaxEvasionDistance = 45
standMinEvasionDistance = 8

local function restoreStandParts()
    for part, defaults in pairs(standPartDefaults) do
        if part and part.Parent and part:IsA("BasePart") then
            part.CanCollide = defaults.canCollide
            part.CanTouch = defaults.canTouch
            part.CanQuery = defaults.canQuery
        end
    end
    standPartDefaults = {}
end

local function setStandGhost(active)
    active = not not active
    if standGhostActive == active then
        return
    end
    standGhostActive = active
    if not standGhostActive and not noclipActive then
        restoreStandParts()
    end
end

function setNoclip(active)
    if noclipActive == active then
        return
    end
    noclipActive = active
    if not noclipActive and not standGhostActive then
        restoreStandParts()
    end
end

RunService.Stepped:Connect(function()
    local char = LocalPlayer.Character
    if not char then
        return
    end

    local needsNoCollide = noclipActive or standGhostActive
    if not needsNoCollide then
        if next(standPartDefaults) ~= nil then
            restoreStandParts()
        end
        return
    end

    for _, part in ipairs(char:GetDescendants()) do
        if part:IsA("BasePart") then
            if standPartDefaults[part] == nil then
                standPartDefaults[part] = {
                    canCollide = part.CanCollide,
                    canTouch = part.CanTouch,
                    canQuery = part.CanQuery,
                }
            end
            if part.CanCollide ~= false then
                part.CanCollide = false
            end

            if standGhostActive then
                if part.CanTouch ~= false then
                    part.CanTouch = false
                end
                if part.CanQuery ~= false then
                    part.CanQuery = false
                end
            else
                local defaults = standPartDefaults[part]
                if defaults then
                    if part.CanTouch ~= defaults.canTouch then
                        part.CanTouch = defaults.canTouch
                    end
                    if part.CanQuery ~= defaults.canQuery then
                        part.CanQuery = defaults.canQuery
                    end
                end
            end
        end
    end
end)

function withNoclip(fn)
    setNoclip(true)
    local ok, err = pcall(fn)
    setNoclip(false)
    if not ok then
        warn(err)
    end
end

local function bindStandHealthMonitor(char)
    if standHealthConn then
        standHealthConn:Disconnect()
        standHealthConn = nil
    end
    if not char then
        return
    end
    local hum = char:FindFirstChildOfClass("Humanoid") or char:WaitForChild("Humanoid", 6)
    if not hum then
        return
    end
    local lastHealth = hum.Health
    standHealthConn = hum.HealthChanged:Connect(function(newHealth)
        if lastHealth and newHealth + 0.05 < lastHealth then
            standLastHitAt = os.clock()
        end
        lastHealth = newHealth
    end)
end

task.defer(function()
    if LocalPlayer and LocalPlayer.Character then
        bindStandHealthMonitor(LocalPlayer.Character)
    end
end)

LocalPlayer.CharacterAdded:Connect(function(char)
    bindStandHealthMonitor(char)
end)

task.spawn(function()
    while task.wait(0.15) do
        if teleporting and not isCalmStandCommandActive() then
            continue
        end
        local now = os.clock()
        local panicGhost = (now - (standLastHitAt or -1e9)) <= (standGhostPanicSeconds or 1.6)
        local calmCommandGhost = isCalmStandCommandActive()
        setStandGhost((panicGhost or calmCommandGhost) and not vehicleMode and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress))
    end
end)

function safeTeleportToShop(root, shopBase)
    if not root or not shopBase then
        return
    end
    root.AssemblyLinearVelocity = Vector3.zero
    root.AssemblyAngularVelocity = Vector3.zero
    root.CFrame = CFrame.new(shopBase.Position + Vector3.new(0, 3, 0))
    task.wait(0.05)
    root.CFrame = CFrame.new(shopBase.Position + Vector3.new(0, -8, 0))
    root.AssemblyLinearVelocity = Vector3.zero
    root.AssemblyAngularVelocity = Vector3.zero
end

local function safeTeleportToCFrame(root, baseCFrame)
    if not root or not baseCFrame then
        return
    end
    local basePos = baseCFrame.Position
    root.AssemblyLinearVelocity = Vector3.zero
    root.AssemblyAngularVelocity = Vector3.zero
    root.CFrame = CFrame.new(basePos + Vector3.new(0, 3, 0))
    task.wait(0.05)
    root.CFrame = CFrame.new(basePos + Vector3.new(0, -8, 0))
    root.AssemblyLinearVelocity = Vector3.zero
    root.AssemblyAngularVelocity = Vector3.zero
end
stomponly = false
getgenv().downonly = false
bringonly = false
takeonly = false
opkill = false
summonTarget = nil
summonMode = "middle"
forceBringDrop = false
deliveryResumeState = nil
pendingGotoTarget = nil
pendingGotoTargetUserId = nil
recentBringReleaseUntil = 0
recentBringReleasedUserId = nil

local function copyListRefs(input)
    local output = {}
    if input then
        for i = 1, #input do
            output[i] = input[i]
        end
    end
    return output
end

local function clearDeliveryResumeState()
    deliveryResumeState = nil
end

local function captureDeliveryResumeState()
    local snapshot = {
        enabled = getgenv().enabled,
        enabled1 = getgenv().enabled1,
        standHomeName = standHomeName,
        targetPlayer = targetPlayer,
        targetPlayerUserId = targetPlayer and targetPlayer.UserId or nil,
        sentrytarget = sentrytarget,
        sentrytargetUserId = sentrytarget and sentrytarget.UserId or nil,
        commandSender = commandSender,
        lockedTarget = lockedTarget,
        lockedTargetUserId = lockedTargetUserId,
        teleporting = teleporting,
        voiding = voiding,
        summonTarget = summonTarget,
        summonTargetUserId = summonTarget and summonTarget.UserId or nil,
        stomponly = stomponly,
        bringonly = bringonly,
        takeonly = takeonly,
        downonly = getgenv().downonly,
        opkill = opkill,
        flingonly = flingonly,
        killall = killall,
        ragebottargets = copyListRefs(ragebottargets),
        shouldSwitch = shouldSwitch,
        currentTargetIndex = currentTargetIndex,
        skyTarget = skyTarget,
        savedTarget5 = savedTarget5,
        gotoPlayer = gotoPlayer,
        gotoCFrame = gotoCFrame,
        gotoTarget = gotoTarget,
        gotoTargetUserId = gotoTargetUserId,
        pendingGotoTarget = pendingGotoTarget,
        pendingGotoTargetUserId = pendingGotoTargetUserId or (pendingGotoTarget and pendingGotoTarget.UserId) or nil,
        vehicleMode = vehicleMode,
        vehicleModel = vehicleModel,
        forceBringDrop = forceBringDrop,
        flameModeActive = flameModeActive,
        flameModeTargetUserId = flameModeTargetUserId,
        flameModeTargetName = flameModeTargetName,
        followTargetId = followState and followState.currentTargetId or nil,
    }

    local hasTask = snapshot.teleporting
        or snapshot.enabled
        or snapshot.enabled1
        or snapshot.lockedTarget ~= nil
        or snapshot.targetPlayer ~= nil
        or snapshot.summonTarget ~= nil
        or snapshot.stomponly
        or snapshot.bringonly
        or snapshot.takeonly
        or snapshot.downonly
        or snapshot.opkill
        or snapshot.flingonly
        or snapshot.killall
        or snapshot.skyTarget ~= nil
        or snapshot.savedTarget5 ~= nil
        or snapshot.gotoCFrame ~= nil
        or snapshot.gotoTarget ~= nil
        or snapshot.pendingGotoTarget ~= nil
        or snapshot.pendingGotoTargetUserId ~= nil
        or snapshot.sentrytarget ~= nil
        or snapshot.vehicleMode
        or snapshot.flameModeActive
        or (#snapshot.ragebottargets > 0)

    if hasTask then
        snapshot.hasTask = true
        deliveryResumeState = snapshot
    else
        deliveryResumeState = nil
    end
end

local function restoreDeliveryResumeState()
    local snapshot = deliveryResumeState
    deliveryResumeState = nil
    if not (snapshot and snapshot.hasTask) then
        return false
    end

    getgenv().enabled = snapshot.enabled
    getgenv().enabled1 = snapshot.enabled1
    standHomeName = snapshot.standHomeName or standHomeName
    targetPlayer = (snapshot.targetPlayerUserId and Players:GetPlayerByUserId(snapshot.targetPlayerUserId)) or snapshot.targetPlayer
    sentrytarget = (snapshot.sentrytargetUserId and Players:GetPlayerByUserId(snapshot.sentrytargetUserId)) or snapshot.sentrytarget
    commandSender = snapshot.commandSender
    lockedTarget = snapshot.lockedTarget
    lockedTargetUserId = snapshot.lockedTargetUserId
    summonTarget = (snapshot.summonTargetUserId and Players:GetPlayerByUserId(snapshot.summonTargetUserId)) or snapshot.summonTarget
    stomponly = snapshot.stomponly
    bringonly = snapshot.bringonly
    takeonly = snapshot.takeonly
    getgenv().downonly = snapshot.downonly
    opkill = snapshot.opkill
    flingonly = snapshot.flingonly
    killall = snapshot.killall
    ragebottargets = copyListRefs(snapshot.ragebottargets)
    shouldSwitch = snapshot.shouldSwitch
    currentTargetIndex = snapshot.currentTargetIndex
    skyTarget = snapshot.skyTarget
    savedTarget5 = snapshot.savedTarget5
    gotoPlayer = snapshot.gotoPlayer
    gotoCFrame = snapshot.gotoCFrame
    gotoTarget = snapshot.gotoTarget
    gotoTargetUserId = snapshot.gotoTargetUserId
    pendingGotoTarget = (snapshot.pendingGotoTargetUserId and Players:GetPlayerByUserId(snapshot.pendingGotoTargetUserId)) or snapshot.pendingGotoTarget
    pendingGotoTargetUserId = snapshot.pendingGotoTargetUserId or (pendingGotoTarget and pendingGotoTarget.UserId) or nil
    vehicleMode = snapshot.vehicleMode
    vehicleModel = snapshot.vehicleModel
    forceBringDrop = snapshot.forceBringDrop
    flameModeActive = snapshot.flameModeActive
    flameModeTargetUserId = snapshot.flameModeTargetUserId
    flameModeTargetName = snapshot.flameModeTargetName
    if followState then
        followState.currentTargetId = snapshot.followTargetId
    end

    teleporting = snapshot.teleporting
    if summonTarget ~= nil then
        hardStop = false
        getgenv().enabled = false
        targetPlayer = nil
        teleporting = false
        voiding = false
    elseif teleporting then
        voiding = false
    else
        voiding = snapshot.voiding
    end

    if getgenv().enabled and standHomeName then
        startFollowingTarget(standHomeName)
        voiding = false
    end

    if #ragebottargets > 0 and (not lockedTarget or not isValidLoopTarget(lockedTarget)) then
        shouldSwitch = true
    end

    return true
end

Players = game:GetService("Players")
player = Players.LocalPlayer
voiding = true
local function isCurrentlyGrabbing()
    local lp = Players.LocalPlayer
    local myChar = lp and lp.Character
    if not myChar then
        return false
    end

    local function hasLocalGrabLink(targetChar)
        local grabConstraint = targetChar and targetChar:FindFirstChild("GRABBING_CONSTRAINT")
        if not grabConstraint then
            return false
        end

        local function isLocalPart(part)
            return part and part:IsA("BasePart") and part:IsDescendantOf(myChar)
        end

        local ok0, part0 = pcall(function() return grabConstraint.Part0 end)
        if ok0 and isLocalPart(part0) then
            return true
        end

        local ok1, part1 = pcall(function() return grabConstraint.Part1 end)
        if ok1 and isLocalPart(part1) then
            return true
        end

        local ok2, att0 = pcall(function() return grabConstraint.Attachment0 end)
        if ok2 and att0 and att0.Parent and att0.Parent:IsDescendantOf(myChar) then
            return true
        end

        local ok3, att1 = pcall(function() return grabConstraint.Attachment1 end)
        if ok3 and att1 and att1.Parent and att1.Parent:IsDescendantOf(myChar) then
            return true
        end

        return false
    end

    if hasLocalGrabLink(myChar) then
        return true
    end

    local ownerPlr = Players:FindFirstChild(Owner)
    local ownerChar = ownerPlr and ownerPlr.Character
    if hasLocalGrabLink(ownerChar) then
        return true
    end

    for _, plr in ipairs(Players:GetPlayers()) do
        local char = plr.Character
        if char and char ~= myChar and char ~= ownerChar and hasLocalGrabLink(char) then
            return true
        end
    end

    return false
end

Players = game:GetService("Players")
player = Players.LocalPlayer
Character = player.Character or player.CharacterAdded:Wait()
hrp = Character:WaitForChild("HumanoidRootPart")

local voidOrbitCenter = nil
local voidOrbitAngle = math.random() * math.pi * 2
local voidOrbitLastTick = os.clock()
local voidOrbitLastCenterRefresh = 0

local function randomVoidCenter()
    return Vector3.new(
        math.random(-950000, 950000),
        math.random(12000, 26000),
        math.random(-950000, 950000)
    )
end

task.spawn(function()
    while true do
        local now = os.clock()
        if voiding
            and summonTarget == nil
            and not autosaveActive
            and os.clock() >= (recentBringReleaseUntil or 0)
            and not isCurrentlyGrabbing()
            and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress)
            and not vehicleMode then
            if not hrp or not hrp.Parent then
                task.wait(standWait(perf.void))
                continue
            end

            local recenterEvery = math.max(voidAuraRecenterSeconds or 7, 2.5)
            local radiusBase = math.max(voidAuraRadius or 120, 40)
            local offCenter = voidOrbitCenter and (hrp.Position - voidOrbitCenter).Magnitude or math.huge
            if (not voidOrbitCenter)
                or hrp.Position.Y < 5000
                or offCenter > (radiusBase * 8)
                or (now - voidOrbitLastCenterRefresh) > recenterEvery then
                if hrp.Position.Y < 5000 or not voidOrbitCenter then
                    voidOrbitCenter = randomVoidCenter()
                else
                    local driftAmount = voidAuraCenterDrift or 20
                    voidOrbitCenter = hrp.Position + Vector3.new(
                        math.random(-driftAmount, driftAmount),
                        math.random(-driftAmount, driftAmount),
                        math.random(-driftAmount, driftAmount)
                    )
                end
                voidOrbitLastCenterRefresh = now
            end

            local delta = math.max(now - (voidOrbitLastTick or now), 1 / 240)
            voidOrbitLastTick = now
            local speed = math.max(voidAuraSpeed or 20, 2)
            voidOrbitAngle = (voidOrbitAngle + speed * delta) % (math.pi * 2)

            local radius = radiusBase + math.sin(now * 3.6) * (voidAuraRadiusJitter or 24)
            radius = math.max(radius, 25)
            local yOffset = math.sin(now * 6.5) * (voidAuraVerticalBob or 10)

            local orbitPos = voidOrbitCenter + Vector3.new(
                math.cos(voidOrbitAngle) * radius,
                yOffset,
                math.sin(voidOrbitAngle) * radius
            )
            local tangentDir = Vector3.new(-math.sin(voidOrbitAngle), 0, math.cos(voidOrbitAngle))
            local lookAtPos = orbitPos + tangentDir * math.max(radius * 0.35, 15)

            hrp.AssemblyLinearVelocity = Vector3.zero
            hrp.AssemblyAngularVelocity = Vector3.zero
            hrp.CFrame = CFrame.lookAt(orbitPos, lookAtPos)
        else
            voidOrbitCenter = nil
            voidOrbitLastTick = now
        end
        task.wait(standWait(perf.void))
    end
end)

player.CharacterAdded:Connect(function(char)
    hrp = char:WaitForChild("HumanoidRootPart")
    if AbuseProtection then
        abuseProtectionCooldownUntil = os.clock() + ABUSE_PROTECTION_RETRY_DELAY
    end
end)

Workspace.FallenPartsDestroyHeight = 0/0

hasSentKOMessage = false

TextChatService = game:GetService("TextChatService")
textChannel = TextChatService.TextChannels:FindFirstChild("RBXGeneral")

TextChatService.ChatWindowConfiguration.Enabled = true

function sendMessage(message)
    if textChannel and message then
        textChannel:SendAsync(message)
    end
end

activationAnnounced = false
task.defer(function()
    if activationAnnounced then
        return
    end
    activationAnnounced = true
    sendMessage("V!N Activated")
end)

sideOffset = 10
local homeFollowState = {
    lastAt = os.clock(),
    phase = math.random() * math.pi * 2,
}

local function resetHomeFollowMotion()
    homeFollowState.lastAt = os.clock()
    homeFollowState.phase = math.random() * math.pi * 2
end

local function getFlatUnit(vector, fallback)
    local flat = Vector3.new(vector.X, 0, vector.Z)
    if flat.Magnitude <= 0.05 then
        return fallback
    end
    return flat.Unit
end

local function getHomeFollowCFrame(playerHRP, targetHRP)
    if not (playerHRP and targetHRP) then
        return nil
    end

    local now = os.clock()
    local deltaTime = clamp(now - (homeFollowState.lastAt or now), 1 / 240, 0.08)
    homeFollowState.lastAt = now
    homeFollowState.phase = (homeFollowState.phase or 0) + (homeFollowMotionSpeed or 4.8) * deltaTime

    local targetVelocity = targetHRP.AssemblyLinearVelocity or targetHRP.Velocity or Vector3.zero
    local flatVelocity = Vector3.new(targetVelocity.X, 0, targetVelocity.Z)
    local speed = flatVelocity.Magnitude

    local facingDirection = getFlatUnit(targetHRP.CFrame.LookVector, Vector3.new(0, 0, -1))
    local travelDirection = speed > 2 and getFlatUnit(flatVelocity, facingDirection) or facingDirection
    local rightDirection = Vector3.new(-travelDirection.Z, 0, travelDirection.X)
    if rightDirection.Magnitude <= 0.05 then
        rightDirection = Vector3.new(1, 0, 0)
    else
        rightDirection = rightDirection.Unit
    end

    local predictionTime = clamp(
        (homeFollowPredictionTime or 0.1) + math.min(speed * 0.0012, 0.05),
        0.04,
        0.18
    )
    local predictedTargetPos = targetHRP.Position + flatVelocity * predictionTime
    local distanceBoost = clamp(speed * 0.02, 0, homeFollowMaxDistanceBoost or 2.4)
    local phase = homeFollowState.phase or 0
    local sideWave = math.sin(phase) * (homeFollowSideWave or 0.72)
    local bobWave = math.sin(phase * 0.55) * (homeFollowBob or 0.12)

    local desiredDistance = (homeFollowDistance or 4.6) + distanceBoost
    local desiredSideOffset = (homeFollowSideOffset or 2.3) + sideWave
    local desiredHeight = (homeFollowHeight or 1.15) + bobWave

    local desiredPos = predictedTargetPos
        - travelDirection * desiredDistance
        + rightDirection * desiredSideOffset
        + Vector3.new(0, desiredHeight, 0)

    local currentPos = playerHRP.Position
    local desiredGap = (desiredPos - currentPos).Magnitude
    local snapDistance = homeFollowSnapDistance or 26
    local farSnapDistance = homeFollowFarSnapDistance or 60
    local followAlpha = clamp(
        (homeFollowCatchup or 0.64) + math.min(desiredGap / math.max(snapDistance, 1), 0.45),
        0.28,
        1
    )

    local finalPos = desiredGap >= farSnapDistance and desiredPos or currentPos:Lerp(desiredPos, followAlpha)
    local lookAtPos = predictedTargetPos
        + Vector3.new(0, homeFollowLookHeight or 1.35, 0)
        + flatVelocity * 0.035

    return CFrame.lookAt(finalPos, lookAtPos)
end

function startFollowingTarget(senderName)
    targetPlayer = game.Players:FindFirstChild(senderName)
    if not targetPlayer then return end
    standHomeName = senderName
    resetHomeFollowMotion()
    local ownerChar = targetPlayer.Character
    local ownerHRP = ownerChar and ownerChar:FindFirstChild("HumanoidRootPart")
    lastOwnerPosition = ownerHRP and ownerHRP.Position or nil
end

local function resumeOwnerFollow()
    if not getgenv().enabled then
        return false
    end
    local followName = standHomeName or Owner
    if followName then
        startFollowingTarget(followName)
    end
    voiding = false
    return true
end

local pendingOwnerFollowResumeName = nil
local pendingKOTaskResumeState = nil
local continueStandTaskAfterRespawn = false
local postResetLoadoutGraceUntil = 0
local handleBrownBagCommand
local handleSmiteCommand
local primeCombatLoadoutAfterRespawn
local resetRespawnFireState
local hasUsableCombatLoadout
local equipRespawnCombatLoadout
local requestImmediateCombatLoadoutPrime
local requestOwnerFollowLoadoutPrimeBurst

local function clearPendingOwnerFollowResume()
    pendingOwnerFollowResumeName = nil
end

local function clearPendingKOTaskResume()
    pendingKOTaskResumeState = nil
    continueStandTaskAfterRespawn = false
end

local function shouldPreserveOwnerFollowOnDeath()
    return getgenv().enabled
        and not hardStop
        and standHomeName ~= nil
        and lockedTarget == nil
        and not stand2Active
        and not bringonly
        and not takeonly
        and not toDeliveryActive
        and not vehicleMode
        and not flameModeActive
        and not stomponly
        and not getgenv().downonly
        and not opkill
        and not flingonly
        and not killall
        and not autosaveActive
        and #ragebottargets == 0
end

local function hasActiveStandTask()
    return smiteCommandInProgress
        or brownBagActionInProgress
        or stand2Active
        or autosaveActive
        or vehicleMode
        or summonTarget ~= nil
        or teleporting
        or shouldSwitch
        or bringonly
        or takeonly
        or toDeliveryActive
        or flameModeActive
        or stomponly
        or getgenv().downonly
        or opkill
        or killall
        or flingonly
        or lockedTarget ~= nil
        or lockedTargetUserId ~= nil
        or sentrytarget ~= nil
        or skyTarget ~= nil
        or savedTarget5 ~= nil
        or gotoPlayer ~= nil
        or gotoCFrame ~= nil
        or gotoTarget ~= nil
        or forceBringDrop
        or (#ragebottargets > 0)
end

local function shouldForceStandOutOfVoid()
    if hardStop then
        return false
    end

    if isManualVoidHoldActive() then
        return false
    end

    if isStandCommandBusy() then
        return true
    end

    if summonTarget ~= nil then
        return true
    end

    if buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingVehicleInProgress or immediateLoadoutPrimeInProgress then
        return true
    end

    if getgenv().enabled and standHomeName ~= nil then
        return true
    end

    return hasActiveStandTask()
end

local function shouldKeepStandIdleInVoid()
    if isManualVoidHoldActive() then
        return true
    end

    if summonTarget ~= nil then
        return false
    end

    if isStandCommandBusy() then
        return false
    end

    if hardStop then
        return true
    end

    if getgenv().enabled and standHomeName ~= nil then
        return false
    end

    if getgenv().enabled1 then
        return true
    end

    if buyingInProgress or buyingGunInProgress or buyingMaskInProgress then
        return false
    end

    return not hasActiveStandTask()
end

local idleVoidFailsafeSince = nil

local function shouldForceIdleVoidFallback()
    if hardStop then
        return true
    end

    if isManualVoidHoldActive() then
        return true
    end

    if summonTarget ~= nil then
        return false
    end

    if getgenv().enabled and standHomeName ~= nil then
        return false
    end

    if buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress or immediateLoadoutPrimeInProgress then
        return false
    end

    if isCurrentlyGrabbing() then
        return false
    end

    return not hasActiveStandTask()
end

local function requestIdleVoidReturn(delayTime)
    task.delay(delayTime or 0.05, function()
        if shouldForceIdleVoidFallback() then
            clearStandCommandBusy()
            voiding = true
        end
    end)
end

local function shouldKeepStandTaskAfterKO()
    if hardStop then
        return false
    end

    return smiteCommandInProgress
        or brownBagActionInProgress
        or getgenv().enabled
        or getgenv().enabled1
        or stand2Active
        or autoSaveEnabled
        or autosaveActive
        or vehicleMode
        or summonTarget ~= nil
        or teleporting
        or shouldSwitch
        or bringonly
        or takeonly
        or toDeliveryActive
        or flameModeActive
        or stomponly
        or getgenv().downonly
        or opkill
        or killall
        or flingonly
        or lockedTarget ~= nil
        or lockedTargetUserId ~= nil
        or sentrytarget ~= nil
        or #ragebottargets > 0
end

local function shouldContinueStandTaskInPlaceAfterKO()
    if hardStop then
        return false
    end

    return shouldPreserveOwnerFollowOnDeath() or shouldKeepStandTaskAfterKO()
end

local function capturePendingKOTaskResume()
    local snapshot = {
        enabled = getgenv().enabled,
        enabled1 = getgenv().enabled1,
        standHomeName = standHomeName,
        targetPlayer = targetPlayer,
        targetPlayerUserId = targetPlayer and targetPlayer.UserId or nil,
        lockedTarget = lockedTarget,
        lockedTargetUserId = lockedTargetUserId,
        autoLocked = autoLocked,
        teleporting = teleporting,
        voiding = voiding,
        summonTarget = summonTarget,
        summonTargetUserId = summonTarget and summonTarget.UserId or nil,
        stomponly = stomponly,
        bringonly = bringonly,
        takeonly = takeonly,
        downonly = getgenv().downonly,
        opkill = opkill,
        flingonly = flingonly,
        killall = killall,
        ragebottargets = copyListRefs(ragebottargets),
        shouldSwitch = shouldSwitch,
        currentTargetIndex = currentTargetIndex,
        skyTarget = skyTarget,
        skyTargetUserId = skyTarget and skyTarget.UserId or nil,
        savedTarget5 = savedTarget5,
        savedTarget5UserId = savedTarget5 and savedTarget5.UserId or nil,
        gotoPlayer = gotoPlayer,
        gotoPlayerUserId = gotoPlayer and gotoPlayer.UserId or nil,
        gotoCFrame = gotoCFrame,
        gotoTarget = gotoTarget,
        gotoTargetUserId = gotoTargetUserId,
        pendingGotoTarget = pendingGotoTarget,
        pendingGotoTargetUserId = pendingGotoTargetUserId or (pendingGotoTarget and pendingGotoTarget.UserId) or nil,
        vehicleMode = vehicleMode,
        vehicleModel = vehicleModel,
        forceBringDrop = forceBringDrop,
        flameModeActive = flameModeActive,
        flameModeTargetUserId = flameModeTargetUserId,
        flameModeTargetName = flameModeTargetName,
        stand2Active = stand2Active,
        stand2TargetName = stand2TargetName,
        stand2TargetUserId = stand2TargetUserId,
        stand2CurrentTarget = stand2CurrentTarget,
        sentrytarget = sentrytarget,
        sentrytargetUserId = sentrytarget and sentrytarget.UserId or nil,
        toDeliveryActive = toDeliveryActive,
        lastToDestination = lastToDestination,
        lastToDropCFrame = lastToDropCFrame,
        commandSender = commandSender,
        autoSaveEnabled = autoSaveEnabled,
        brownBagActionInProgress = brownBagActionInProgress,
        brownBagTargetName = brownBagTargetName,
        smiteCommandInProgress = smiteCommandInProgress,
        smiteTargetUserId = smiteTargetUserId,
        smiteTargetName = smiteTargetName,
        deliveryResumeState = deliveryResumeState,
    }

    local hasTask = snapshot.enabled
        or snapshot.enabled1
        or snapshot.lockedTarget ~= nil
        or snapshot.lockedTargetUserId ~= nil
        or snapshot.summonTarget ~= nil
        or snapshot.stomponly
        or snapshot.bringonly
        or snapshot.takeonly
        or snapshot.downonly
        or snapshot.opkill
        or snapshot.flingonly
        or snapshot.killall
        or snapshot.skyTarget ~= nil
        or snapshot.savedTarget5 ~= nil
        or snapshot.gotoCFrame ~= nil
        or snapshot.gotoTarget ~= nil
        or snapshot.pendingGotoTarget ~= nil
        or snapshot.pendingGotoTargetUserId ~= nil
        or snapshot.vehicleMode
        or snapshot.flameModeActive
        or snapshot.stand2Active
        or snapshot.sentrytarget ~= nil
        or snapshot.toDeliveryActive
        or snapshot.autoSaveEnabled
        or snapshot.brownBagActionInProgress
        or snapshot.smiteCommandInProgress
        or (#snapshot.ragebottargets > 0)

    if hasTask then
        snapshot.hasTask = true
        pendingKOTaskResumeState = snapshot
        return true
    end

    pendingKOTaskResumeState = nil
    return false
end

local function shouldForcePostResetCombatRecovery(snapshot)
    if not snapshot then
        return false
    end

    return snapshot.enabled1
        or snapshot.stand2Active
        or snapshot.flameModeActive
        or snapshot.stomponly
        or snapshot.bringonly
        or snapshot.takeonly
        or snapshot.downonly
        or snapshot.opkill
        or snapshot.killall
        or snapshot.toDeliveryActive
        or snapshot.lockedTarget ~= nil
        or snapshot.lockedTargetUserId ~= nil
        or snapshot.sentrytarget ~= nil
        or (#snapshot.ragebottargets > 0)
end

local function queueOwnerFollowResume()
    local followName = standHomeName
    if not followName and targetPlayer then
        followName = targetPlayer.Name
    end
    if not followName then
        followName = Owner
    end
    pendingOwnerFollowResumeName = followName
end

local function tryResumePendingOwnerFollow(character)
    local followName = pendingOwnerFollowResumeName
    if not followName then
        return
    end
    if hardStop then
        clearPendingOwnerFollowResume()
        return
    end

    task.delay(0.35, function()
        if pendingOwnerFollowResumeName ~= followName then
            return
        end
        if hardStop then
            clearPendingOwnerFollowResume()
            return
        end
        local localPlayer = Players.LocalPlayer
        if not localPlayer or localPlayer.Character ~= character then
            return
        end

        getgenv().enabled = true
        standHomeName = followName
        targetPlayer = nil
        teleporting = false
        voiding = false
        startFollowingTarget(followName)
        reloadTool()
        clearPendingOwnerFollowResume()
    end)
end

local function tryResumePendingKOTask(character)
    local snapshot = pendingKOTaskResumeState
    if not (snapshot and snapshot.hasTask) then
        return
    end
    if hardStop then
        clearPendingKOTaskResume()
        return
    end

    task.delay(0.45, function()
        if pendingKOTaskResumeState ~= snapshot then
            return
        end
        if hardStop then
            clearPendingKOTaskResume()
            return
        end
        local localPlayer = Players.LocalPlayer
        if not localPlayer or localPlayer.Character ~= character then
            return
        end

        local resumeBrownBagTarget = snapshot.brownBagActionInProgress and snapshot.brownBagTargetName or nil
        local resumeSmiteTarget = snapshot.smiteCommandInProgress and (snapshot.smiteTargetName or snapshot.lockedTarget and snapshot.lockedTarget.Name) or nil

        if resumeBrownBagTarget then
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
            clearPendingOwnerFollowResume()
            clearPendingKOTaskResume()
            task.defer(function()
                handleBrownBagCommand(resumeBrownBagTarget)
            end)
            return
        end

        if resumeSmiteTarget then
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
            clearPendingOwnerFollowResume()
            clearPendingKOTaskResume()
            task.defer(function()
                handleSmiteCommand(resumeSmiteTarget)
            end)
            return
        end

        getgenv().enabled = snapshot.enabled
        getgenv().enabled1 = snapshot.enabled1
        standHomeName = snapshot.standHomeName or standHomeName or Owner
        targetPlayer = (snapshot.targetPlayerUserId and Players:GetPlayerByUserId(snapshot.targetPlayerUserId)) or snapshot.targetPlayer
        lockedTarget = (snapshot.lockedTargetUserId and Players:GetPlayerByUserId(snapshot.lockedTargetUserId)) or snapshot.lockedTarget
        lockedTargetUserId = snapshot.lockedTargetUserId
        autoLocked = snapshot.autoLocked
        summonTarget = (snapshot.summonTargetUserId and Players:GetPlayerByUserId(snapshot.summonTargetUserId)) or snapshot.summonTarget
        stomponly = snapshot.stomponly
        bringonly = snapshot.bringonly
        takeonly = snapshot.takeonly
        getgenv().downonly = snapshot.downonly
        opkill = snapshot.opkill
        flingonly = snapshot.flingonly
        killall = snapshot.killall
        ragebottargets = copyListRefs(snapshot.ragebottargets)
        shouldSwitch = snapshot.shouldSwitch
        currentTargetIndex = snapshot.currentTargetIndex
        skyTarget = (snapshot.skyTargetUserId and Players:GetPlayerByUserId(snapshot.skyTargetUserId)) or snapshot.skyTarget
        savedTarget5 = (snapshot.savedTarget5UserId and Players:GetPlayerByUserId(snapshot.savedTarget5UserId)) or snapshot.savedTarget5
        gotoPlayer = (snapshot.gotoPlayerUserId and Players:GetPlayerByUserId(snapshot.gotoPlayerUserId)) or snapshot.gotoPlayer
        gotoCFrame = snapshot.gotoCFrame
        gotoTarget = (snapshot.gotoTargetUserId and Players:GetPlayerByUserId(snapshot.gotoTargetUserId)) or snapshot.gotoTarget
        gotoTargetUserId = snapshot.gotoTargetUserId or (gotoTarget and gotoTarget.UserId) or nil
        pendingGotoTarget = (snapshot.pendingGotoTargetUserId and Players:GetPlayerByUserId(snapshot.pendingGotoTargetUserId)) or snapshot.pendingGotoTarget
        pendingGotoTargetUserId = snapshot.pendingGotoTargetUserId or (pendingGotoTarget and pendingGotoTarget.UserId) or nil
        vehicleMode = snapshot.vehicleMode
        vehicleModel = snapshot.vehicleModel
        forceBringDrop = snapshot.forceBringDrop
        flameModeActive = snapshot.flameModeActive
        flameModeTargetUserId = snapshot.flameModeTargetUserId
        flameModeTargetName = snapshot.flameModeTargetName
        stand2Active = snapshot.stand2Active
        stand2TargetName = snapshot.stand2TargetName
        stand2TargetUserId = snapshot.stand2TargetUserId
        stand2CurrentTarget = (snapshot.stand2TargetUserId and Players:GetPlayerByUserId(snapshot.stand2TargetUserId)) or snapshot.stand2CurrentTarget
        sentrytarget = (snapshot.sentrytargetUserId and Players:GetPlayerByUserId(snapshot.sentrytargetUserId)) or snapshot.sentrytarget
        toDeliveryActive = snapshot.toDeliveryActive
        lastToDestination = snapshot.lastToDestination
        lastToDropCFrame = snapshot.lastToDropCFrame
        commandSender = snapshot.commandSender
        autoSaveEnabled = snapshot.autoSaveEnabled
        autosaveActive = false
        deliveryResumeState = snapshot.deliveryResumeState

        teleporting = snapshot.teleporting
        if teleporting then
            voiding = false
        else
            voiding = snapshot.voiding
        end

        if getgenv().enabled and standHomeName then
            startFollowingTarget(standHomeName)
            voiding = false
        end

        if #ragebottargets > 0 and (not lockedTarget or not isValidLoopTarget(lockedTarget)) then
            shouldSwitch = true
        end

        if shouldForcePostResetCombatRecovery(snapshot) then
            postResetCombatRecoveryActive = true
            postResetCombatRecoveryUntil = os.clock() + 9
        else
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
        end

        resetFollowPrediction()
        reloadTool()
        if primeCombatLoadoutAfterRespawn then
            primeCombatLoadoutAfterRespawn(character)
        end
        clearPendingOwnerFollowResume()
        clearPendingKOTaskResume()
    end)
end

local function tryContinueStandTaskAfterRespawn(character)
    if not continueStandTaskAfterRespawn then
        return
    end

    continueStandTaskAfterRespawn = false
    task.delay(0.35, function()
        local localPlayer = Players.LocalPlayer
        if not localPlayer or localPlayer.Character ~= character or hardStop then
            return
        end

        if getgenv().enabled and standHomeName then
            if not targetPlayer or not targetPlayer:IsDescendantOf(game) then
                targetPlayer = Players:FindFirstChild(standHomeName)
            end
            startFollowingTarget(standHomeName)
            voiding = false
        elseif teleporting
            or stand2Active
            or flameModeActive
            or getgenv().enabled1
            or summonTarget ~= nil
            or bringonly
            or takeonly
            or stomponly
            or getgenv().downonly
            or opkill
            or flingonly
            or killall
            or lockedTarget ~= nil
            or sentrytarget ~= nil
            or toDeliveryActive
            or (#ragebottargets > 0) then
            voiding = false
        end

        if getgenv().enabled1
            or stand2Active
            or flameModeActive
            or stomponly
            or bringonly
            or takeonly
            or getgenv().downonly
            or opkill
            or killall
            or toDeliveryActive
            or lockedTarget ~= nil
            or lockedTargetUserId ~= nil
            or sentrytarget ~= nil
            or (#ragebottargets > 0) then
            postResetCombatRecoveryActive = true
            postResetCombatRecoveryUntil = os.clock() + 9
        else
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
        end

        resetFollowPrediction()

        if primeCombatLoadoutAfterRespawn then
            primeCombatLoadoutAfterRespawn(character)
        else
            reloadTool()
        end
    end)
end

function reloadTool()
    local player = game.Players.LocalPlayer
    local character = player.Character
    if not character then
        return
    end
    for _, tool in ipairs(character:GetChildren()) do
        if tool:IsA("Tool") then
            tryReloadTool(tool)
        end
    end
end

function handleLoopKillCommand(targetName, specificBot)
    targetName = targetName:lower()
    if specificBot then
        specificBot = specificBot:lower()
    end

    local localPlayer = Players.LocalPlayer
    if not localPlayer then return end

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            if specificBot and not botKey:lower():find(specificBot, 1, true) then
                return
            end
            reloadTool()
            lockedTarget = nil
            stomponly = false
            bringonly = false
            takeonly = false
            getgenv().downonly = false
            opkill = false
            voiding = false
            summonTarget = nil
            flingonly = false

            for _, targetPlayer in ipairs(Players:GetPlayers()) do
                local targetPlayerName = targetPlayer.Name:lower()
                local targetDisplayName = targetPlayer.DisplayName:lower()

                if targetPlayerName:find(targetName, 1, true) or targetDisplayName:find(targetName, 1, true) then
                    lockedTarget = targetPlayer
                    return
                end
            end
        end
    end
end

function handleStompCommand(targetName, specificBot)
    targetName = targetName:lower()
    if specificBot then
        specificBot = specificBot:lower()
    end

    local localPlayer = Players.LocalPlayer
    if not localPlayer then return end

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            if specificBot and not botKey:lower():find(specificBot, 1, true) then
                return
            end
            reloadTool()
            lockedTarget = nil
            stomponly = true
            bringonly = false
            takeonly = false
            getgenv().downonly = false
            opkill = false
            voiding = false
            summonTarget = nil
            flingonly = false

            for _, targetPlayer in ipairs(Players:GetPlayers()) do
                local targetPlayerName = targetPlayer.Name:lower()
                local targetDisplayName = targetPlayer.DisplayName:lower()

                if targetPlayerName:find(targetName, 1, true) or targetDisplayName:find(targetName, 1, true) then
                    lockedTarget = targetPlayer
                    return
                end
            end
        end
    end
end

function handleOPKillCommand(targetName, specificBot)
    targetName = targetName:lower()
    if specificBot then
        specificBot = specificBot:lower()
    end

    local localPlayer = Players.LocalPlayer
    if not localPlayer then return end

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            if specificBot and not botKey:lower():find(specificBot, 1, true) then
                return
            end
            reloadTool()
            lockedTarget = nil
            stomponly = false
            bringonly = false
            takeonly = false
            getgenv().downonly = false
            opkill = true
            voiding = false
            summonTarget = nil
            flingonly = false

            for _, targetPlayer in ipairs(Players:GetPlayers()) do
                local targetPlayerName = targetPlayer.Name:lower()
                local targetDisplayName = targetPlayer.DisplayName:lower()

                if targetPlayerName:find(targetName, 1, true) or targetDisplayName:find(targetName, 1, true) then
                    lockedTarget = targetPlayer
                    return
                end
            end
        end
    end
end

function handleFlingCommand(targetName)
    targetName = targetName:lower()
    local localPlayer = Players.LocalPlayer
    if not localPlayer then return end

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            reloadTool()
            lockedTarget = nil
            stomponly = false
            bringonly = false
            takeonly = false
            getgenv().downonly = false
            opkill = false
            voiding = false
            summonTarget = nil
            flingonly = true

            for _, targetPlayer in ipairs(Players:GetPlayers()) do
                local tName = targetPlayer.Name:lower()
                local tDisplay = targetPlayer.DisplayName:lower()
                if tName:find(targetName, 1, true) or tDisplay:find(targetName, 1, true) then
                    lockedTarget = targetPlayer
                    return
                end
            end
        end
    end
end

function handleBringCommand(targetName, specificBot, senderName)
    commandSender = senderName
    targetName = targetName:lower()
    if specificBot then
        specificBot = specificBot:lower()
    end

    local localPlayer = Players.LocalPlayer
    if not localPlayer then return end

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            if specificBot and not botKey:lower():find(specificBot, 1, true) then
                return
            end
            reloadTool()
            lockedTarget = nil
            stomponly = false
            bringonly = true
            takeonly = false
            getgenv().downonly = false
            opkill = false
            voiding = false
            summonTarget = nil
            flingonly = false

            for _, targetPlayer in ipairs(Players:GetPlayers()) do
                local targetPlayerName = targetPlayer.Name:lower()
                local targetDisplayName = targetPlayer.DisplayName:lower()

                if targetPlayerName:find(targetName, 1, true) or targetDisplayName:find(targetName, 1, true) then
                    lockedTarget = targetPlayer
                    return
                end
            end
        end
    end
end

savedTarget5 = nil

function handleTakeCommand(targetName, destinationName)
    targetName = targetName:lower()
    if destinationName then
        destinationName = destinationName:lower()
    end

    local targetPlayer = nil
    for _, player in ipairs(game.Players:GetPlayers()) do
        if player.Name:lower() == targetName then
            targetPlayer = player
            break
        end
    end

    local destinationPlayer = nil
    if destinationName then
        for _, player in ipairs(game.Players:GetPlayers()) do
            if player.Name:lower() == destinationName then
                destinationPlayer = player
                savedTarget5 = destinationPlayer
                break
            end
        end
    end

    for _, player in ipairs(Players:GetPlayers()) do
        local playerName = player.Name:lower()
        local playerDisplayName = player.DisplayName:lower()

        if playerName:find(targetName, 1, true) or playerDisplayName:find(targetName, 1, true) then
            targetPlayer = player
        end

        if playerName:find(destinationName, 1, true) or playerDisplayName:find(destinationName, 1, true) then
            destinationPlayer = player
        end

        if targetPlayer and destinationPlayer then
            break
        end
    end

    if targetPlayer and destinationPlayer then
        savedTarget5 = destinationPlayer

        lockedTarget = targetPlayer
        reloadTool()
        stomponly = false
        bringonly = false
        getgenv().downonly = false
        opkill = false
        voiding = false
        takeonly = true
        summonTarget = nil
        flingonly = false
    end
end

gotoPlayer = nil
gotoCFrame = nil
gotoTarget = nil
gotoTargetUserId = nil
-- Pending target/cframe for goto actions that should only be applied after a successful grab
pendingGotoTarget = nil
pendingGotoTargetUserId = nil
vehicleMode = false
vehicleSeatCFrame = CFrame.new(-866.932, 21.179, -587.317) * CFrame.Angles(math.rad(178.53), math.rad(-70.483), math.rad(178.615))
vehiclePickupPos = Vector3.new(-897.034, 18.355, -611.24)
vehicleSeatName = "VehicleSeat"
passengerSeatName = "Seat"
vehicleName = "KOALA12345A3BIKE"
vehicleShopName = "[FoodsCart] - $17"
vehiclePurchaseEnabled = false
lastVehiclePurchase = 0
lastVehicleSearch = 0
vehicleModel = nil

function handleGotoCommand(playerName, locationName)
    local Players = game:GetService("Players")
    local player = Players:FindFirstChild(playerName)
    if not player then return end

    locationName = locationName:lower()

    gotoCFrame = locationCFrames[locationName]
    gotoTarget = nil
    
    -- If not a location, try to find a player
    if not gotoCFrame then
        local targetPlayer = findPlayerByPartial(locationName)
        if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
            gotoTarget = targetPlayer
        else
            return
        end
    end

    gotoPlayer = player
    vehicleMode = true
    vehicleModel = nil
    lockedTarget = nil
    reloadTool()
    stomponly = false
    bringonly = false
    getgenv().downonly = false
    opkill = false
    voiding = false
    takeonly = false
    summonTarget = nil
    flingonly = false
end

skyTarget = nil

function handleSkyCommand(username)
    local Players = game:GetService("Players")
    local target = Players:FindFirstChild(username)
    if not target then return end

    skyTarget = target
    lockedTarget = target

    reloadTool()
    stomponly = false
    bringonly = false
    getgenv().downonly = false
    opkill = false
    voiding = false
    takeonly = true
    summonTarget = nil
    flingonly = false
end

function handleDownCommand(targetName, specificBot)
    targetName = targetName:lower()
    if specificBot then
        specificBot = specificBot:lower()
    end

    local localPlayer = Players.LocalPlayer
    if not localPlayer then return end

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            if specificBot and not botKey:lower():find(specificBot, 1, true) then
                return
            end
            reloadTool()
            lockedTarget = nil
            stomponly = false
            bringonly = false
            takeonly = false
            getgenv().downonly = true
            opkill = false
            voiding = false
            summonTarget = nil
            flingonly = false

            for _, targetPlayer in ipairs(Players:GetPlayers()) do
                local targetPlayerName = targetPlayer.Name:lower()
                local targetDisplayName = targetPlayer.DisplayName:lower()

                if targetPlayerName:find(targetName, 1, true) or targetDisplayName:find(targetName, 1, true) then
                    lockedTarget = targetPlayer
                    return
                end
            end
        end
    end
end

local RESET_SOURCE = {
    Repair = "repair",
    Manual = "reset",
    Death = "death",
}

local AUTO_PREKO_RESET_HEALTH = 8
local AUTO_KO_RESET_DELAY = 0.01
local ABUSE_PROTECTION_RETRY_DELAY = 3.2
local koResetConnection
local preKoResetConnection
local autoPreKOResetPending = false
local abuseProtectionCooldownUntil = 0

local function canTriggerAbuseProtection()
    return AbuseProtection
        and not autoPreKOResetPending
        and os.clock() >= (abuseProtectionCooldownUntil or 0)
end

local function shouldTriggerAbuseProtection(myCharacter, targetCharacter, isReloading)
    if not canTriggerAbuseProtection() then
        return false
    end

    if refreshingfakeposition or isReloading or not (myCharacter and targetCharacter) then
        return false
    end

    local myHumanoid = myCharacter:FindFirstChildOfClass("Humanoid")
    local myRoot = myCharacter:FindFirstChild("HumanoidRootPart")
    local targetRoot = targetCharacter:FindFirstChild("HumanoidRootPart")
    local myForceField = myCharacter:FindFirstChildOfClass("ForceField")
    local targetForceField = targetCharacter:FindFirstChildOfClass("ForceField")

    if not myHumanoid or myHumanoid.Health <= 0 then
        return false
    end

    if myForceField or not targetForceField or not (myRoot and targetRoot) then
        return false
    end

    return (myRoot.Position - targetRoot.Position).Magnitude <= 30
end

local function killLocalCharacter(resetDelay, expectedCharacter)
    local delayTime = math.max(resetDelay or 0, 0)
    task.delay(delayTime, function()
        local localPlayer = Players.LocalPlayer
        local currentCharacter = localPlayer and localPlayer.Character
        if expectedCharacter and currentCharacter ~= expectedCharacter then
            autoPreKOResetPending = false
            return
        end
        local humanoid = currentCharacter and currentCharacter:FindFirstChildOfClass("Humanoid")
        if humanoid and humanoid.Health > 0 then
            humanoid.Health = 0
        end
        autoPreKOResetPending = false
    end)
end

local function resetStandState(resetSource)
    local source = resetSource or RESET_SOURCE.Manual
    local preserveOwnerFollow = source == RESET_SOURCE.Death and shouldPreserveOwnerFollowOnDeath()
    local preserveTaskState = source == RESET_SOURCE.Death and shouldKeepStandTaskAfterKO() and not preserveOwnerFollow
    local continueTaskInPlace = source == RESET_SOURCE.Death and shouldContinueStandTaskInPlaceAfterKO()

    invalidateToDeliveryRun()
    postResetCombatRecoveryActive = false
    postResetCombatRecoveryUntil = 0

    if continueTaskInPlace then
        clearPendingOwnerFollowResume()
        clearPendingKOTaskResume()
        continueStandTaskAfterRespawn = true

        local localPlayer = Players.LocalPlayer
        local character = localPlayer and localPlayer.Character
        autoPreKOResetPending = true
        killLocalCharacter(AUTO_KO_RESET_DELAY, character)
        return
    end

    if preserveTaskState then
        capturePendingKOTaskResume()
    else
        clearPendingKOTaskResume()
    end

    if preserveOwnerFollow then
        queueOwnerFollowResume()
    else
        clearPendingOwnerFollowResume()
    end

    cancelSmiteCommandState()
    getgenv().enabled = false
    getgenv().enabled1 = false
    ragebottargets = {}
    shouldSwitch = false
    currentTargetIndex = 1
    lockedTarget = nil
    lockedTargetUserId = nil
    autoLocked = false
    sentrytarget = nil
    skyTarget = nil
    autodrop = false
    stand2Active = false
    stand2TargetName = nil
    stand2TargetUserId = nil
    stand2CurrentTarget = nil
    flameModeActive = false
    flameModeTargetUserId = nil
    flameModeTargetName = nil
    brownBagActionInProgress = false
    brownBagTargetName = nil
    buyingInProgress = false
    buyingGunInProgress = false
    buyingMaskInProgress = false
    voiding = true
    summonTarget = nil
    stomponly = false
    bringonly = false
    takeonly = false
    getgenv().downonly = false
    opkill = false
    flingonly = false
    killall = false
    savedTarget5 = nil
    gotoPlayer = nil
    gotoCFrame = nil
    gotoTarget = nil
    gotoTargetUserId = nil
    pendingGotoTarget = nil
    pendingGotoTargetUserId = nil
    vehicleMode = false
    vehicleModel = nil
    forceBringDrop = false
    commandSender = nil
    teleporting = false
    autosaveActive = false
    lastToDestination = nil
    toDeliveryActive = false
    lastToDropCFrame = nil
    resetBringGrabAttemptState()
    clearDeliveryResumeState()
    if source == RESET_SOURCE.Repair then
        local localPlayer = Players.LocalPlayer
        local character = localPlayer and localPlayer.Character
        killLocalCharacter(0, character)
    elseif source == RESET_SOURCE.Death then
        local localPlayer = Players.LocalPlayer
        local character = localPlayer and localPlayer.Character
        autoPreKOResetPending = true
        killLocalCharacter(AUTO_KO_RESET_DELAY, character)
    end
end

local function tryStandReset(specificBot, resetSource)
    local localPlayer = Players.LocalPlayer
    if not localPlayer then
        return
    end

    resetSource = resetSource or RESET_SOURCE.Manual

    for botKey, botUsername in pairs(Bots) do
        if localPlayer.Name:lower() == botUsername:lower() then
            if specificBot and not botKey:lower():find(specificBot, 1, true) then
                return
            end

            resetStandState(resetSource)
            return
        end
    end
end

local function watchCharacterForKO(character)
    if not character then
        return
    end
    autoPreKOResetPending = false
    local bodyEffects = character:FindFirstChild("BodyEffects") or character:WaitForChild("BodyEffects", 3)
    if not bodyEffects then
        return
    end
    local humanoid = character:FindFirstChildOfClass("Humanoid") or character:WaitForChild("Humanoid", 3)
    local koValue = bodyEffects:FindFirstChild("K.O") or bodyEffects:WaitForChild("K.O", 3)
    if not koValue then
        return
    end
    if koResetConnection then
        koResetConnection:Disconnect()
        koResetConnection = nil
    end
    if preKoResetConnection then
        preKoResetConnection:Disconnect()
        preKoResetConnection = nil
    end
    koResetConnection = koValue:GetPropertyChangedSignal("Value"):Connect(function()
        if not koValue.Value then
            return
        end
        if autoPreKOResetPending then
            return
        end
        tryStandReset(nil, RESET_SOURCE.Death)
    end)
    if humanoid then
        preKoResetConnection = humanoid.HealthChanged:Connect(function(newHealth)
            if autoPreKOResetPending then
                return
            end
            if newHealth <= 0 or newHealth > AUTO_PREKO_RESET_HEALTH then
                return
            end
            if koValue.Value then
                return
            end
            tryStandReset(nil, RESET_SOURCE.Death)
        end)
    end
end

function handleFixCommand(specificBot)
    if specificBot then
        specificBot = specificBot:lower()
    end
    tryStandReset(specificBot, RESET_SOURCE.Repair)
end

function handleResetCommand(specificBot)
    if specificBot then
        specificBot = specificBot:lower()
    end
    tryStandReset(specificBot, RESET_SOURCE.Manual)
end

watchCharacterForKO(Player.Character)
Player.CharacterAdded:Connect(watchCharacterForKO)
Player.CharacterAdded:Connect(tryContinueStandTaskAfterRespawn)
Player.CharacterAdded:Connect(tryResumePendingKOTask)
Player.CharacterAdded:Connect(tryResumePendingOwnerFollow)
Player.CharacterAdded:Connect(function(character)
    if hasActiveCombatRecoveryTask() then
        bootstrapCombatAfterRespawn(character)
    else
        task.delay(0.2, function()
            if Players.LocalPlayer and Players.LocalPlayer.Character == character and hasActiveCombatRecoveryTask() then
                bootstrapCombatAfterRespawn(character)
            end
        end)
    end
end)

player = game.Players.LocalPlayer
character = player.Character
AnimationId = "rbxassetid://507766388"
overrideMovementAnimations = false
autoEmoteEnabled = false

animations = {
    {"run", "RunAnim"},
    {"walk", "WalkAnim"},
    {"jump", "JumpAnim"},
    {"fall", "FallAnim"},
    {"climb", "ClimbAnim"}
}

player.CharacterAdded:Connect(function(character)
    if not overrideMovementAnimations then
        return
    end
    local animateScript = character:WaitForChild("Animate")

    for _, pair in pairs(animations) do
        local parentName, animName = pair[1], pair[2]
        local parent = animateScript:FindFirstChild(parentName)
        if parent then
            local anim = parent:FindFirstChild(animName)
            if anim then
                anim.AnimationId = AnimationId
            end
        end
    end
end)

EMOTES = {
    ["billy bounce"] = "rbxassetid://136095999219650",
    ["zero two dance v2"] = "rbxassetid://116714406076290",
    ["jabba switchway"] = "rbxassetid://82682811348660",
    ["beat"] = "rbxassetid://133394554631338"
}

player = game.Players.LocalPlayer
character = player.Character
currentTrack = nil
emoteLoopTask = nil

function playAnimation(animId)
    if not character then return end
    local humanoid = character:WaitForChild("Humanoid", 10)
    local animator = humanoid:WaitForChild("Animator", 10)

    if currentTrack then
        currentTrack:Stop()
        currentTrack = nil
    end

    local animation = Instance.new("Animation")
    animation.AnimationId = animId
    local track = animator:LoadAnimation(animation)
    track.Looped = true
    track.Priority = Enum.AnimationPriority.Action4
    track:Play()
    currentTrack = track
end

function startEmoteLoop()
    if emoteLoopTask then
        task.cancel(emoteLoopTask)
        emoteLoopTask = nil
    end
    if not autoEmoteEnabled then
        if currentTrack then
            currentTrack:Stop()
            currentTrack = nil
        end
        return
    end

    emoteLoopTask = task.spawn(function()
        while character and character.Parent do
            local emoteIds = {}
            for _, animId in pairs(EMOTES) do
                table.insert(emoteIds, animId)
            end
            local chosenEmote = emoteIds[math.random(1, #emoteIds)]
            playAnimation(chosenEmote)
            task.wait(30)
        end
    end)
end

if character then
    startEmoteLoop()
end

player.CharacterAdded:Connect(function(newChar)
    character = newChar
    if currentTrack then
        currentTrack:Stop()
        currentTrack = nil
    end
    startEmoteLoop()
end)

local SUMMON_SONG_ID = "76973204445042"
local SUMMON_SONG_DELAY = 4
local summonMusicToken = 0
local SUMMON_BOOMBOX_OWNER = "7xil0_0"

local function getSongIdVariants(songId)
    local textId = tostring(songId)
    local numericId = tonumber(songId)
    local variants = {
        textId,
        "rbxassetid://" .. textId,
        "http://www.roblox.com/asset/?id=" .. textId,
    }

    if numericId then
        table.insert(variants, numericId)
    end

    return variants
end

local function getStandBoombox()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    if not localPlayer then
        return nil
    end

    local preferredPlayer = players:FindFirstChild(SUMMON_BOOMBOX_OWNER)
    if preferredPlayer then
        local preferredCharacterBoombox = preferredPlayer.Character and preferredPlayer.Character:FindFirstChild("[Boombox]")
        if preferredCharacterBoombox then
            return preferredCharacterBoombox
        end

        local preferredBackpack = preferredPlayer:FindFirstChild("Backpack")
        if preferredBackpack then
            local preferredBackpackBoombox = preferredBackpack:FindFirstChild("[Boombox]")
            if preferredBackpackBoombox then
                return preferredBackpackBoombox
            end
        end
    end

    local characterBoombox = localPlayer.Character and localPlayer.Character:FindFirstChild("[Boombox]")
    if characterBoombox then
        return characterBoombox
    end

    local backpack = localPlayer:FindFirstChild("Backpack")
    if backpack then
        return backpack:FindFirstChild("[Boombox]")
    end

    return nil
end

local function setBoomboxLoopedState(looped)
    local boombox = getStandBoombox()
    if not boombox then
        return
    end

    for _, descendant in ipairs(boombox:GetDescendants()) do
        if descendant:IsA("Sound") then
            descendant.Looped = looped and true or false
        end
    end
end

local function stopBoomboxPlayback(boombox)
    if not boombox then
        return
    end

    local mainEvent = ReplicatedStorage and ReplicatedStorage:FindFirstChild("MainEvent")
    if mainEvent then
        pcall(function()
            mainEvent:FireServer("Boombox", "")
        end)
        pcall(function()
            mainEvent:FireServer("Boombox", 0)
        end)
        pcall(function()
            mainEvent:FireServer("PlayBoombox", "")
        end)
        pcall(function()
            mainEvent:FireServer("PlayBoombox", 0)
        end)
        pcall(function()
            mainEvent:FireServer("PlaySong", "")
        end)
        pcall(function()
            mainEvent:FireServer("PlaySong", 0)
        end)
        pcall(function()
            mainEvent:FireServer("StopBoombox")
        end)
        pcall(function()
            mainEvent:FireServer("BoomboxStop")
        end)
        pcall(function()
            mainEvent:FireServer("StopSong")
        end)
    end

    for _, descendant in ipairs(boombox:GetDescendants()) do
        local lowerName = descendant.Name:lower()
        if descendant:IsA("TextBox") then
            descendant.Text = ""
        elseif descendant:IsA("StringValue") then
            if lowerName:find("id", 1, true) or lowerName:find("song", 1, true) or lowerName:find("sound", 1, true) then
                descendant.Value = ""
            end
        elseif descendant:IsA("IntValue") or descendant:IsA("NumberValue") then
            if lowerName:find("id", 1, true) or lowerName:find("song", 1, true) or lowerName:find("sound", 1, true) then
                descendant.Value = 0
            end
        end
    end

    for _, descendant in ipairs(boombox:GetDescendants()) do
        if descendant:IsA("Sound") then
            descendant.Looped = false
            descendant.Playing = false
            descendant.TimePosition = 0
            pcall(function()
                descendant:Stop()
            end)
        elseif descendant:IsA("RemoteEvent") then
            pcall(function()
                descendant:FireServer("")
            end)
            pcall(function()
                descendant:FireServer(0)
            end)
        elseif descendant:IsA("BindableEvent") then
            pcall(function()
                descendant:Fire("")
            end)
            pcall(function()
                descendant:Fire(0)
            end)
        end
    end

    pcall(function()
        boombox:Deactivate()
    end)
end

local function playSummonSongOnce(songId)
    local localPlayer = game.Players.LocalPlayer
    if not localPlayer then
        return
    end

    local characterModel = localPlayer.Character
    local humanoid = characterModel and characterModel:FindFirstChildOfClass("Humanoid")
    local boombox = getStandBoombox()
    local backpack = localPlayer:FindFirstChild("Backpack")
    local currentToken = summonMusicToken

    if not (characterModel and humanoid and boombox and backpack) then
        return
    end

    setBoomboxLoopedState(false)

    if boombox.Parent ~= characterModel then
        pcall(function()
            humanoid:EquipTool(boombox)
        end)
        task.wait(0.25)
    end

    local songIdVariants = getSongIdVariants(songId)

    for _, descendant in ipairs(boombox:GetDescendants()) do
        local lowerName = descendant.Name:lower()
        if descendant:IsA("TextBox") then
            descendant.Text = tostring(songIdVariants[1])
        elseif descendant:IsA("StringValue") then
            if lowerName:find("id", 1, true) or lowerName:find("song", 1, true) or lowerName:find("sound", 1, true) then
                descendant.Value = tostring(songIdVariants[2] or songIdVariants[1])
            end
        elseif descendant:IsA("IntValue") or descendant:IsA("NumberValue") then
            if lowerName:find("id", 1, true) or lowerName:find("song", 1, true) or lowerName:find("sound", 1, true) then
                local numericId = tonumber(songId)
                if numericId then
                    descendant.Value = numericId
                end
            end
        end
    end

    local mainEvent = ReplicatedStorage and ReplicatedStorage:FindFirstChild("MainEvent")
    if mainEvent then
        for _, variant in ipairs(songIdVariants) do
            pcall(function()
                mainEvent:FireServer("Boombox", variant)
            end)
            pcall(function()
                mainEvent:FireServer("PlayBoombox", variant)
            end)
            pcall(function()
                mainEvent:FireServer("PlaySong", variant)
            end)
        end
    end

    for _, descendant in ipairs(boombox:GetDescendants()) do
        if descendant:IsA("RemoteEvent") then
            for _, variant in ipairs(songIdVariants) do
                pcall(function()
                    descendant:FireServer(variant)
                end)
            end
        elseif descendant:IsA("BindableEvent") then
            for _, variant in ipairs(songIdVariants) do
                pcall(function()
                    descendant:Fire(variant)
                end)
            end
        end
    end

    pcall(function()
        boombox:Activate()
    end)
    task.wait(0.08)
    pcall(function()
        boombox:Activate()
    end)

    task.delay(SUMMON_SONG_DELAY, function()
        if summonMusicToken ~= currentToken then
            return
        end
        stopBoomboxPlayback(boombox)
        if boombox.Parent ~= backpack then
            pcall(function()
                boombox.Parent = backpack
            end)
        end
    end)
end

local function queueSummonSong()
    summonMusicToken = summonMusicToken + 1
    local currentToken = summonMusicToken
    task.spawn(function()
        if summonMusicToken ~= currentToken then
            return
        end
        if not summonTarget then
            return
        end
        playSummonSongOnce(SUMMON_SONG_ID)
    end)
end

function handleTeleportCommand(targetName, specificBot)
    hardStop = false
    getgenv().enabled = false
    getgenv().enabled1 = false
    stand2Active = false
    targetPlayer = nil
    ragebottargets = {}
    shouldSwitch = false
    currentTargetIndex = 1
    lockedTarget = nil
    lockedTargetUserId = nil
    autoLocked = false
    sentrytarget = nil
    skyTarget = nil
    savedTarget5 = nil
    teleporting = false
    stomponly = false
    bringonly = false
    takeonly = false
    getgenv().downonly = false
    opkill = false
    flingonly = false
    killall = false
    voiding = false
    summonTarget = Players:FindFirstChild(targetName)
    queueSummonSong()
end

function handleHideCommand(specificBot)
    -- .v should ALWAYS stop everything immediately, regardless of which combat command is active.
    -- We keep the `specificBot` argument for compatibility, but we intentionally ignore it.

    local localPlayer = game.Players.LocalPlayer
    if not localPlayer then return end
    local preserveOwnerControls = {
        sentry = getgenv().enabled1,
        autoSaveEnabled = autoSaveEnabled,
        abuseProtection = AbuseProtection,
    }

    -- HARD STOP LATCH: prevents loops from re-acquiring targets / resuming.
    hardStop = true
    activateManualVoidHold()
    clearStandCommandBusy()
    invalidateToDeliveryRun()
    cancelSmiteCommandState()
    clearPendingOwnerFollowResume()
    clearPendingKOTaskResume()
    postResetCombatRecoveryActive = false
    postResetCombatRecoveryUntil = 0

    -- HARD STOP: cancel all modes and send stand to void.
    getgenv().enabled = false

    -- cancel any combat/loop targets
    ragebottargets = {}
    shouldSwitch = false
    currentTargetIndex = 1

    -- clear all targeting + relock state
    lockedTarget = nil
    lockedTargetUserId = nil
    autoLocked = false
    summonMusicToken = summonMusicToken + 1
    sentrytarget = nil
    skyTarget = nil

    -- disable ALL mode flags
    stomponly = false
    bringonly = false
    takeonly = false
    getgenv().downonly = false
    opkill = false
    flingonly = false
    killall = false
    vehicleMode = false

    -- IMPORTANT: clear stored destinations / carry logic that can keep moving the stand
    savedTarget5 = nil
    gotoPlayer = nil
    gotoCFrame = nil
    gotoTarget = nil
    gotoTargetUserId = nil
    pendingGotoTarget = nil
    pendingGotoTargetUserId = nil
    lastToDestination = nil
    toDeliveryActive = false
    lastToDropCFrame = nil
    vehicleModel = nil
    forceBringDrop = false
    commandSender = nil
    resetBringGrabAttemptState()
    clearDeliveryResumeState()

    -- stop movement tasks
    teleporting = false
    summonTarget = nil

    -- turn off stand2 if it was enabled
    stand2Active = false
    stand2TargetName = nil
    stand2TargetUserId = nil
    stand2CurrentTarget = nil
    flameModeActive = false
    flameModeTargetUserId = nil
    flameModeTargetName = nil
    brownBagActionInProgress = false
    brownBagTargetName = nil
    autosaveActive = false

    -- force void/idle
    voiding = true

    -- best-effort: drop anything currently grabbed, then reload
    pcall(function()
        if not autosaveActive then
            ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
        end
    end)
    reloadTool()

    -- Keep owner toggle-style options alive after the manual stop.
    getgenv().enabled1 = preserveOwnerControls.sentry and true or false
    autoSaveEnabled = preserveOwnerControls.autoSaveEnabled and true or false
    AbuseProtection = preserveOwnerControls.abuseProtection and true or false

    if preserveOwnerControls.sentry or preserveOwnerControls.autoSaveEnabled or preserveOwnerControls.abuseProtection then
        hardStop = false
    end
end

task.spawn(function()
    while true do
        if summonTarget and not summonTarget:IsDescendantOf(game) then
            summonTarget = nil
        end

        if shouldKeepStandIdleInVoid() and summonTarget == nil then
            voiding = true
        end

        if getgenv().enabled and (not targetPlayer or not targetPlayer:IsDescendantOf(game)) and standHomeName then
            targetPlayer = game.Players:FindFirstChild(standHomeName)
            if targetPlayer then
                resetHomeFollowMotion()
            end
        end

        if getgenv().enabled and targetPlayer and player.Character and targetPlayer.Character and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            voiding = false
            local playerHRP = player.Character:FindFirstChild("HumanoidRootPart")
            local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if playerHRP and targetHRP then
                local desiredCFrame = getHomeFollowCFrame(playerHRP, targetHRP)
                if desiredCFrame then
                    local myChar = player.Character
                    if myChar then
                        myChar:PivotTo(desiredCFrame)
                    else
                        playerHRP.CFrame = desiredCFrame
                    end
                    playerHRP.Velocity = Vector3.zero
                    playerHRP.RotVelocity = Vector3.zero
                    playerHRP.AssemblyLinearVelocity = Vector3.zero
                    playerHRP.AssemblyAngularVelocity = Vector3.zero
                    lastOwnerPosition = targetHRP.Position
                end
            end
        end
        task.wait(standWait(perf.loop))
    end
end)

task.spawn(function()
    while true do
        if shouldForceIdleVoidFallback() then
            local now = os.clock()
            idleVoidFailsafeSince = idleVoidFailsafeSince or now

            if not isStandCommandBusy() then
                voiding = true
            elseif (now - idleVoidFailsafeSince) >= 0.9 then
                clearStandCommandBusy()
                voiding = true
            end
        else
            idleVoidFailsafeSince = nil
        end
        task.wait(0.1)
    end
end)

task.spawn(function()
    while true do
        if shouldForceStandOutOfVoid() then
            voiding = false
        end
        task.wait(standWait(perf.loop))
    end
end)

Players = game:GetService("Players")
localPlayer = game.Players.LocalPlayer
player = game.Players.LocalPlayer
character = player.Character or player.CharacterAdded:Wait()
humanoid = character:FindFirstChildOfClass("Humanoid")

localPlayer.CharacterAdded:Connect(function(newCharacter)
    character = newCharacter
end)

function teleportToTarget(commandSender)
    local targetPlayer = game.Players:FindFirstChild(commandSender)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        local targetPosition = targetPlayer.Character.HumanoidRootPart.Position
        local myHRP = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if myHRP then
            lockedTarget = nil
            voiding = false
            summonTarget = nil
            myHRP.Velocity = Vector3.zero
            myHRP.RotVelocity = Vector3.zero
            myHRP.AssemblyLinearVelocity = Vector3.zero
            myHRP.AssemblyAngularVelocity = Vector3.zero
            myHRP.CFrame = CFrame.new(
                targetPosition.X + -5,
                targetPosition.Y,
                targetPosition.Z
            )
            myHRP.Velocity = Vector3.zero
            myHRP.RotVelocity = Vector3.zero
            myHRP.AssemblyLinearVelocity = Vector3.zero
            myHRP.AssemblyAngularVelocity = Vector3.zero
        end
    end
end

function teleportToPosition(targetPosition)
    local player = game.Players.LocalPlayer
    if not player or not player.Character then return end
    local hrp = player.Character:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    hrp.Velocity = Vector3.zero
    hrp.RotVelocity = Vector3.zero
    hrp.AssemblyLinearVelocity = Vector3.zero
    hrp.AssemblyAngularVelocity = Vector3.zero
    hrp.CFrame = CFrame.new(targetPosition)
    hrp.Velocity = Vector3.zero
    hrp.RotVelocity = Vector3.zero
    hrp.AssemblyLinearVelocity = Vector3.zero
    hrp.AssemblyAngularVelocity = Vector3.zero
end

local SKY_DROP_HEIGHT = 120
local DROP_OFFSET = Vector3.new(0, -2, 0)
local DROP_BACK_OFFSET = Vector3.new(0, 6, -10)
local GRAB_CONFIRM_DISTANCE = 18
local GRAB_CONFIRM_TIME = 0.2
local GRAB_FALLBACK_DISTANCE = 28
local GRAB_FALLBACK_WINDOW = 1.2
local GRAB_RETRY_ROUNDS = 3
local GRAB_RETRY_SETTLE = 0.03
local GRAB_RECHECK_WAIT = 0.06
local DROP_RELEASE_ATTEMPTS = 6
local DROP_RELEASE_WAIT = 0.05
local DROP_MOVE_ATTEMPTS = 8
local DROP_SYNC_TIMEOUT = 1.1
local STRICT_DROP_STAND_DISTANCE = 10
local STRICT_DROP_CARRIED_DISTANCE = 13
local STRICT_DROP_POST_RELEASE_PIN_LOOPS = 10
local STRICT_DROP_POST_RELEASE_PIN_WAIT = 0.03
STRICT_DROP_FORCE_RELEASE_ATTEMPTS = 4
STRICT_DROP_FORCE_RELEASE_WAIT = 0.04
STRICT_DROP_FORCE_RELEASE_EXIT_LOOPS = 6
local STRICT_DROP_RELEASE_STAND_DISTANCE = 5.5
local STRICT_DROP_RELEASE_CARRIED_DISTANCE = 7
local STRICT_DROP_RELEASE_CONFIRM_LOOPS = 4
local STRICT_DROP_RELEASE_CONFIRM_WAIT = 0.025
local FAST_BRING_GRAB_ROUNDS = 7
local FAST_BRING_SYNC_TIMEOUT = 0.48
local FAST_BRING_STAND_DISTANCE = 14
local FAST_BRING_CARRIED_DISTANCE = 18
local FAST_BRING_HOVER_HEIGHT = 5.0
local FAST_BRING_SETTLE_HEIGHT = 2.6
local FAST_BRING_RELEASE_ATTEMPTS = 8
local FAST_BRING_RELEASE_WAIT = 0.05
local FAST_BRING_PIN_LOOPS = 10
local FAST_BRING_PIN_WAIT = 0.02
local FAST_BRING_PIN_DISTANCE = 10
local FAST_BRING_FINAL_STAND_DISTANCE = 8
local FAST_BRING_FINAL_CARRIED_DISTANCE = 5
local FAST_BRING_POST_RELEASE_PIN_LOOPS = 14
local FAST_BRING_POST_RELEASE_PIN_WAIT = 0.03
local FAST_BRING_ATTACH_CONFIRM_LOOPS = 18
local FAST_BRING_ATTACH_CONFIRM_WAIT = 0.04
local FAST_BRING_ATTACH_CONFIRM_DISTANCE = 16
local BRING_STRICT_ATTACH_DISTANCE = 16
local BRING_GRAB_LOCKOUT_TIME = 0.35
local OWNER_BRING_PRE_RELEASE_PIN_LOOPS = 16
local OWNER_BRING_PRE_RELEASE_PIN_WAIT = 0.03
local OWNER_BRING_POST_RELEASE_PIN_LOOPS = 22
local OWNER_BRING_POST_RELEASE_PIN_WAIT = 0.04
local OWNER_BRING_POST_RELEASE_REQUIRED_HITS = 5
local OWNER_BRING_FINAL_TARGET_DISTANCE = 4
local OWNER_BRING_DIRECT_RELEASE_RETRIES = 3
local OWNER_BRING_DIRECT_REPIN_LOOPS = 8
local OWNER_BRING_DIRECT_REPIN_WAIT = 0.025
local BRING_TARGET_GRAB_ROUNDS = 14
local BRING_TARGET_GRAB_SETTLE = 0.055
local BRING_TARGET_GRAB_RECHECK_WAIT = 0.14
local BRING_TARGET_GRAB_HARDLOCK_ROUNDS = 16
local BRING_TARGET_GRAB_HARDLOCK_SETTLE = 0.065
local BRING_TARGET_GRAB_HARDLOCK_RECHECK_WAIT = 0.16
local DELIVERY_OWNER_GRAB_ROUNDS = 14
local DELIVERY_OWNER_GRAB_SETTLE = 0.055
local DELIVERY_OWNER_GRAB_RECHECK_WAIT = 0.14
local DELIVERY_OWNER_GRAB_HARDLOCK_ROUNDS = 18
local DELIVERY_OWNER_GRAB_HARDLOCK_SETTLE = 0.065
local DELIVERY_OWNER_GRAB_HARDLOCK_RECHECK_WAIT = 0.18
local DROP_RAY_START = 6
local DROP_RAY_DEPTH = 300
local DROP_GROUND_CLEARANCE = 0.5
DropDebug = true
local grabSeenAt = setmetatable({}, {__mode = "k"})
local grabAttemptAt = setmetatable({}, {__mode = "k"})
local GRAB_APPROACH_OFFSETS = {
    Vector3.new(0, 3.55, 0),
    Vector3.new(0, 3.1, 0),
    Vector3.new(0, 4.05, 0),
    Vector3.new(1.15, 3.25, 0),
    Vector3.new(-1.15, 3.25, 0),
    Vector3.new(0, 3.25, 1.15),
    Vector3.new(0, 3.25, -1.15),
    Vector3.new(0.7, 3.7, 0.7),
    Vector3.new(-0.7, 3.7, -0.7),
}
local AUTOSAVE_GRAB_APPROACH_OFFSETS = {
    Vector3.new(0, 2.7, 0),
    Vector3.new(0, 2.25, 0),
    Vector3.new(0, 1.85, 0),
    Vector3.new(0.9, 2.1, 0),
    Vector3.new(-0.9, 2.1, 0),
    Vector3.new(0, 2.1, 0.9),
    Vector3.new(0, 2.1, -0.9),
    Vector3.new(0.65, 2.5, 0.65),
    Vector3.new(-0.65, 2.5, -0.65),
    Vector3.new(1.2, 1.95, 0),
    Vector3.new(-1.2, 1.95, 0),
}
local AUTOSAVE_GRAB_HARDLOCK_OFFSETS = {
    Vector3.new(0, 2.0, 0),
    Vector3.new(0, 1.7, 0),
    Vector3.new(0, 1.45, 0),
    Vector3.new(0.45, 1.85, 0),
    Vector3.new(-0.45, 1.85, 0),
    Vector3.new(0, 1.85, 0.45),
    Vector3.new(0, 1.85, -0.45),
    Vector3.new(0.8, 1.7, 0),
    Vector3.new(-0.8, 1.7, 0),
    Vector3.new(0, 1.7, 0.8),
    Vector3.new(0, 1.7, -0.8),
}
local BRING_TARGET_GRAB_APPROACH_OFFSETS = {
    Vector3.new(0, 2.95, 0),
    Vector3.new(0, 2.45, 0),
    Vector3.new(0, 2.0, 0),
    Vector3.new(0, 1.7, 0),
    Vector3.new(1.0, 2.2, 0),
    Vector3.new(-1.0, 2.2, 0),
    Vector3.new(0, 2.2, 1.0),
    Vector3.new(0, 2.2, -1.0),
    Vector3.new(0.75, 2.6, 0.75),
    Vector3.new(-0.75, 2.6, -0.75),
    Vector3.new(1.3, 2.0, 0),
    Vector3.new(-1.3, 2.0, 0),
    Vector3.new(0, 2.0, 1.3),
    Vector3.new(0, 2.0, -1.3),
}
local BRING_TARGET_GRAB_HARDLOCK_OFFSETS = {
    Vector3.new(0, 2.15, 0),
    Vector3.new(0, 1.85, 0),
    Vector3.new(0, 1.55, 0),
    Vector3.new(0.5, 1.95, 0),
    Vector3.new(-0.5, 1.95, 0),
    Vector3.new(0, 1.95, 0.5),
    Vector3.new(0, 1.95, -0.5),
    Vector3.new(0.9, 1.8, 0),
    Vector3.new(-0.9, 1.8, 0),
    Vector3.new(0, 1.8, 0.9),
    Vector3.new(0, 1.8, -0.9),
}
local OWNER_BRING_GRAB_ROUNDS = 6
local OWNER_BRING_GRAB_SETTLE = 0.03
local OWNER_BRING_GRAB_RECHECK_WAIT = 0.06
local OWNER_BRING_GRAB_HARDLOCK_ROUNDS = 8
local OWNER_BRING_GRAB_HARDLOCK_SETTLE = 0.04
local OWNER_BRING_GRAB_HARDLOCK_RECHECK_WAIT = 0.08
local OWNER_BRING_GRAB_APPROACH_OFFSETS = {
    Vector3.new(0, 2.15, 0),
    Vector3.new(0, 1.9, 0),
    Vector3.new(0, 1.6, 0),
    Vector3.new(0, 1.35, 0),
    Vector3.new(0.65, 1.95, 0),
    Vector3.new(-0.65, 1.95, 0),
    Vector3.new(0, 1.95, 0.65),
    Vector3.new(0, 1.95, -0.65),
    Vector3.new(0.95, 1.8, 0),
    Vector3.new(-0.95, 1.8, 0),
    Vector3.new(0.55, 1.55, 0),
    Vector3.new(-0.55, 1.55, 0),
    Vector3.new(0, 1.55, 0.55),
    Vector3.new(0, 1.55, -0.55),
}
local OWNER_BRING_GRAB_HARDLOCK_OFFSETS = {
    Vector3.new(0, 1.95, 0),
    Vector3.new(0, 1.72, 0),
    Vector3.new(0, 1.48, 0),
    Vector3.new(0, 1.28, 0),
    Vector3.new(0.42, 1.84, 0),
    Vector3.new(-0.42, 1.84, 0),
    Vector3.new(0, 1.84, 0.42),
    Vector3.new(0, 1.84, -0.42),
    Vector3.new(0.62, 1.62, 0),
    Vector3.new(-0.62, 1.62, 0),
    Vector3.new(0, 1.62, 0.62),
    Vector3.new(0, 1.62, -0.62),
    Vector3.new(0.34, 1.32, 0),
    Vector3.new(-0.34, 1.32, 0),
}
local DELIVERY_OWNER_GRAB_APPROACH_OFFSETS = {
    Vector3.new(0, 2.8, 0),
    Vector3.new(0, 2.35, 0),
    Vector3.new(0, 1.95, 0),
    Vector3.new(0, 1.6, 0),
    Vector3.new(0.95, 2.15, 0),
    Vector3.new(-0.95, 2.15, 0),
    Vector3.new(0, 2.15, 0.95),
    Vector3.new(0, 2.15, -0.95),
    Vector3.new(0.7, 2.55, 0.7),
    Vector3.new(-0.7, 2.55, -0.7),
    Vector3.new(1.25, 1.95, 0),
    Vector3.new(-1.25, 1.95, 0),
    Vector3.new(0, 1.95, 1.25),
    Vector3.new(0, 1.95, -1.25),
}
local DELIVERY_OWNER_GRAB_HARDLOCK_OFFSETS = {
    Vector3.new(0, 2.2, 0),
    Vector3.new(0, 1.9, 0),
    Vector3.new(0, 1.65, 0),
    Vector3.new(0.45, 2.0, 0),
    Vector3.new(-0.45, 2.0, 0),
    Vector3.new(0, 2.0, 0.45),
    Vector3.new(0, 2.0, -0.45),
    Vector3.new(0.8, 1.9, 0),
    Vector3.new(-0.8, 1.9, 0),
    Vector3.new(0, 1.9, 0.8),
    Vector3.new(0, 1.9, -0.8),
}
local DELIVERY_OWNER_GRAB_PART_NAMES = {
    "HumanoidRootPart",
    "UpperTorso",
    "Torso",
    "Head",
}
local BRING_TARGET_GRAB_PART_NAMES = {
    "HumanoidRootPart",
    "UpperTorso",
    "Torso",
    "Head",
}
local OWNER_BRING_GRAB_PART_NAMES = {
    "HumanoidRootPart",
    "UpperTorso",
    "Torso",
    "Head",
}
local BRING_KO_ATTEMPT_INTERVAL = 0.14
local BRING_KO_ATTEMPTS = 8
local BRING_KO_WAIT = 0.06
local AUTOSAVE_ATTACH_CONFIRM_LOOPS = 12
local AUTOSAVE_ATTACH_CONFIRM_WAIT = 0.03
local AUTOSAVE_ATTACH_CONFIRM_DISTANCE = 12
local lastBringKOAttemptAt = {}

local function isCharacterKO(targetChar)
    local bodyEffects = targetChar and targetChar:FindFirstChild("BodyEffects")
    local koValue = bodyEffects and bodyEffects:FindFirstChild("K.O")
    return koValue and koValue.Value or false
end

local function forceCharacterKO(targetChar, attempts, waitTime)
    if not targetChar then
        return false
    end
    if isCharacterKO(targetChar) then
        return true
    end

    local hum = targetChar:FindFirstChildOfClass("Humanoid")
    if not hum then
        return false
    end

    for _ = 1, math.max(attempts or BRING_KO_ATTEMPTS, 1) do
        if isCharacterKO(targetChar) then
            return true
        end
        pcall(function()
            hum.Health = 0
            hum:ChangeState(Enum.HumanoidStateType.Dead)
        end)
        task.wait(waitTime or BRING_KO_WAIT)
    end

    return isCharacterKO(targetChar)
end

local function tryForceBringKO(targetPlayer, interval)
    if not (targetPlayer and targetPlayer.Character) then
        return false
    end

    local userId = targetPlayer.UserId or 0
    local now = os.clock()
    local minInterval = interval or BRING_KO_ATTEMPT_INTERVAL
    if userId ~= 0 and (now - (lastBringKOAttemptAt[userId] or 0)) < minInterval then
        return false
    end

    if userId ~= 0 then
        lastBringKOAttemptAt[userId] = now
    end
    return forceCharacterKO(targetPlayer.Character, BRING_KO_ATTEMPTS, BRING_KO_WAIT)
end

local function getSkyDropCFrame(baseCFrame, ownerPlayer)
    if not baseCFrame then
        return nil
    end

    local basePos = baseCFrame.Position
    local targetY = basePos.Y + SKY_DROP_HEIGHT

    if ownerPlayer and ownerPlayer.Character then
        local ownerHRP = ownerPlayer.Character:FindFirstChild("HumanoidRootPart")
        if ownerHRP then
            -- Keep drop above owner height to avoid underground spawns.
            targetY = math.max(targetY, ownerHRP.Position.Y + 30)
        end
    end

    return CFrame.new(basePos.X, targetY, basePos.Z)
end

local function getStandHeight(ownerChar)
    if not ownerChar then
        return 0
    end
    local hrp = ownerChar:FindFirstChild("HumanoidRootPart")
    local hum = ownerChar:FindFirstChildOfClass("Humanoid")
    if not (hrp and hum) then
        return 0
    end
    local halfHeight = (hrp.Size and hrp.Size.Y or 0) * 0.5
    local hipHeight = hum.HipHeight or 0
    return halfHeight + hipHeight + DROP_GROUND_CLEARANCE
end

local function getDropCFrame(baseCFrame, ownerChar)
    if not baseCFrame then
        return nil
    end
    local basePos = baseCFrame.Position
    local targetY = basePos.Y

    local params = RaycastParams.new()
    params.FilterType = Enum.RaycastFilterType.Blacklist
    local ignore = {}
    local lp = game.Players.LocalPlayer
    if lp and lp.Character then
        table.insert(ignore, lp.Character)
    end
    if ownerChar then
        table.insert(ignore, ownerChar)
    end
    params.FilterDescendantsInstances = ignore

    -- Raycast vertically downwards from the target position to find ground
    local rayOrigin = basePos + Vector3.new(0, 50, 0)
    local rayDirection = Vector3.new(0, -DROP_RAY_DEPTH, 0)
    local hit = workspace:Raycast(rayOrigin, rayDirection, params)
    
    local finalY = targetY
    if hit and hit.Position then
        local groundY = hit.Position.Y
        -- Place Owner directly on ground with minimal offset
        -- Just add a small clearance to prevent clipping
        finalY = groundY + DROP_GROUND_CLEARANCE
        
        -- Ensure we never exceed the target Y
        finalY = math.min(targetY, finalY)
    end

    return CFrame.new(basePos.X, finalY, basePos.Z)
end

local function getDropExitCFrame(baseCFrame)
    if not baseCFrame then
        return nil
    end
    local basePos = baseCFrame.Position
    return CFrame.new(basePos + DROP_BACK_OFFSET)
end

local deliveryPositionCache = {}

local function getPlayerDestinationPart(targetPlayer)
    local targetChar = targetPlayer and targetPlayer.Character
    if not targetChar then
        return nil
    end
    return targetChar:FindFirstChild("HumanoidRootPart")
        or targetChar:FindFirstChild("UpperTorso")
        or targetChar:FindFirstChild("Torso")
        or targetChar:FindFirstChild("Head")
end

local function getPlayerDestinationCFrame(targetPlayer)
    local targetPart = getPlayerDestinationPart(targetPlayer)
    if targetPart then
        local pos = targetPart.Position
        local userId = targetPlayer and targetPlayer.UserId
        if userId then
            deliveryPositionCache[userId] = pos
        end
        return CFrame.new(pos), pos
    end

    local userId = targetPlayer and targetPlayer.UserId
    local cachedPos = userId and deliveryPositionCache[userId] or nil
    if cachedPos then
        return CFrame.new(cachedPos), cachedPos
    end

    return nil, nil
end

local function resolveActiveDeliveryDropState()
    local destinationBaseCFrame = nil
    local destinationPos = nil

    if gotoTarget then
        destinationBaseCFrame, destinationPos = getPlayerDestinationCFrame(gotoTarget)
    end

    if (not destinationBaseCFrame) and lastToDestination then
        local savedLocation = locationCFrames[lastToDestination:lower()]
        if savedLocation then
            destinationBaseCFrame = savedLocation
            destinationPos = savedLocation.Position
        else
            local targetPlayer = resolveDeliveryTargetPlayer(lastToDestination)
            if targetPlayer then
                gotoTarget = targetPlayer
                gotoTargetUserId = targetPlayer.UserId
                destinationBaseCFrame, destinationPos = getPlayerDestinationCFrame(targetPlayer)
            end
        end
    end

    if (not destinationBaseCFrame) and lastToDropCFrame then
        destinationBaseCFrame = lastToDropCFrame
        destinationPos = lastToDropCFrame.Position
    end

    return destinationBaseCFrame, destinationPos
end

local isNearPosition
local isStrictlyAttachedToStand

local function isStrictDeliveryReadyForRelease(standHRP, carriedHRP, targetChar, maxStandDistance, maxCarriedDistance)
    local destinationBaseCFrame, destinationPos = resolveActiveDeliveryDropState()
    if not destinationPos then
        return false, destinationBaseCFrame, destinationPos
    end

    local standReady = standHRP and isNearPosition(
        standHRP,
        destinationPos,
        maxStandDistance or STRICT_DROP_STAND_DISTANCE
    ) or false

    local carriedReady = carriedHRP and isNearPosition(
        carriedHRP,
        destinationPos,
        maxCarriedDistance or STRICT_DROP_CARRIED_DISTANCE
    ) or false

    if targetChar and not isStrictlyAttachedToStand(targetChar, BRING_STRICT_ATTACH_DISTANCE + 4) then
        carriedReady = false
    end

    return standReady and carriedReady, destinationBaseCFrame, destinationPos
end

local function isStrictDeliveryReadyForReleaseStable(standHRP, carriedHRP, targetChar, maxStandDistance, maxCarriedDistance, confirmLoops, confirmWait)
    local loops = math.max(confirmLoops or STRICT_DROP_RELEASE_CONFIRM_LOOPS, 1)
    local pauseTime = confirmWait or STRICT_DROP_RELEASE_CONFIRM_WAIT
    local lastBaseCFrame = nil
    local lastPos = nil

    for attempt = 1, loops do
        local ready, baseCFrame, destinationPos = isStrictDeliveryReadyForRelease(
            standHRP,
            carriedHRP,
            targetChar,
            maxStandDistance or STRICT_DROP_RELEASE_STAND_DISTANCE,
            maxCarriedDistance or STRICT_DROP_RELEASE_CARRIED_DISTANCE
        )
        lastBaseCFrame = baseCFrame or lastBaseCFrame
        lastPos = destinationPos or lastPos
        if not ready then
            return false, lastBaseCFrame, lastPos
        end
        if attempt < loops then
            task.wait(pauseTime)
        end
    end

    return true, lastBaseCFrame, lastPos
end

local function logDrop(msg)
    if DropDebug then
        print("[DROP] " .. msg)
    end
end

local function isPositionClear(pos, ownerChar)
    local boxSize = Vector3.new(4, 6, 4)
    if ownerChar then
        local hrp = ownerChar:FindFirstChild("HumanoidRootPart")
        if hrp and hrp.Size then
            boxSize = hrp.Size + Vector3.new(2, 4, 2)
        end
    end
    local params = OverlapParams.new()
    params.FilterType = Enum.RaycastFilterType.Blacklist
    local ignore = {}
    local lp = game.Players.LocalPlayer
    if lp and lp.Character then
        table.insert(ignore, lp.Character)
    end
    if ownerChar then
        table.insert(ignore, ownerChar)
    end
    params.FilterDescendantsInstances = ignore
    local parts = workspace:GetPartBoundsInBox(CFrame.new(pos), boxSize, params)
    if #parts > 0 then
        return false, "overlap collision"
    end
    return true
end

local function getIndoorDropCFrame(targetPlayer, ownerChar)
    if not (targetPlayer and targetPlayer.Character) then
        return nil
    end
    local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not targetHRP then
        return nil
    end

    local basePos = targetHRP.Position
    local angles = {0, 45, 90, 135, 180, 225, 270, 315}
    local radii = {0, 1.5, 2.5, 3}

    local params = RaycastParams.new()
    params.FilterType = Enum.RaycastFilterType.Blacklist
    params.IgnoreWater = true
    local ignore = {}
    local lp = game.Players.LocalPlayer
    if lp and lp.Character then
        table.insert(ignore, lp.Character)
    end
    table.insert(ignore, targetPlayer.Character)
    if ownerChar then
        table.insert(ignore, ownerChar)
    end
    params.FilterDescendantsInstances = ignore

    local function tryPos(pos)
        local rayOrigin = pos + Vector3.new(0, 4, 0)
        local rayDir = Vector3.new(0, -10, 0)
        local hit = workspace:Raycast(rayOrigin, rayDir, params)
        if not (hit and hit.Instance and hit.Instance:IsA("BasePart") and hit.Instance.CanCollide) then
            logDrop(("no floor hit at (%.2f, %.2f, %.2f)"):format(pos.X, pos.Y, pos.Z))
            return nil
        end
        local floorY = hit.Position.Y + DROP_GROUND_CLEARANCE
        local finalPos = Vector3.new(pos.X, floorY, pos.Z)

        local roofOrigin = finalPos + Vector3.new(0, 2, 0)
        local roofHit = workspace:Raycast(roofOrigin, Vector3.new(0, 4, 0), params)
        if roofHit and roofHit.Instance and roofHit.Instance:IsA("BasePart") and roofHit.Instance.CanCollide then
            local roofDist = (roofHit.Position - roofOrigin).Magnitude
            if roofDist < 2.5 then
                logDrop(("blocked by roof at (%.2f, %.2f, %.2f)"):format(finalPos.X, finalPos.Y, finalPos.Z))
                return nil
            end
        end

        local ok, reason = isPositionClear(finalPos, ownerChar)
        if not ok then
            logDrop(("%s at (%.2f, %.2f, %.2f)"):format(reason, finalPos.X, finalPos.Y, finalPos.Z))
            return nil
        end

        return CFrame.new(finalPos)
    end

    for _, r in ipairs(radii) do
        for _, a in ipairs(angles) do
            local rad = math.rad(a)
            local offset = Vector3.new(math.cos(rad), 0, math.sin(rad)) * r
            local candidate = basePos + offset
            local cf = tryPos(candidate)
            if cf then
                logDrop(("indoor drop ok at (%.2f, %.2f, %.2f)"):format(cf.Position.X, cf.Position.Y, cf.Position.Z))
                return cf
            end
        end
    end

    -- Fallbacks around target (behind/side/above) but still near target.
    local look = targetHRP.CFrame.LookVector
    local right = targetHRP.CFrame.RightVector
    local fallbackOffsets = {
        -look * 2.5,
        right * 2.5,
        -right * 2.5,
        Vector3.new(0, 3, 0),
    }
    for _, off in ipairs(fallbackOffsets) do
        local cf = tryPos(basePos + off)
        if cf then
            logDrop(("fallback drop ok at (%.2f, %.2f, %.2f)"):format(cf.Position.X, cf.Position.Y, cf.Position.Z))
            return cf
        end
    end

    logDrop("indoor drop failed; no safe position found")
    return nil
end

local function resetPartVelocity(part)
    if not part then
        return
    end
    part.Velocity = Vector3.zero
    part.RotVelocity = Vector3.zero
    part.AssemblyLinearVelocity = Vector3.zero
    part.AssemblyAngularVelocity = Vector3.zero
end

local function isConstraintLinkedToLocal(constraint, localChar)
    if not (constraint and localChar) then
        return false
    end

    local function isLocalPart(part)
        return part and part:IsA("BasePart") and part:IsDescendantOf(localChar)
    end

    local ok, part0 = pcall(function() return constraint.Part0 end)
    if ok and isLocalPart(part0) then
        return true
    end
    local ok2, part1 = pcall(function() return constraint.Part1 end)
    if ok2 and isLocalPart(part1) then
        return true
    end

    local ok3, att0 = pcall(function() return constraint.Attachment0 end)
    if ok3 and att0 and att0.Parent and att0.Parent:IsDescendantOf(localChar) then
        return true
    end
    local ok4, att1 = pcall(function() return constraint.Attachment1 end)
    if ok4 and att1 and att1.Parent and att1.Parent:IsDescendantOf(localChar) then
        return true
    end

    return false
end

local function cframeWithPosition(cf, pos)
    if not cf then
        return CFrame.new(pos)
    end
    return CFrame.new(pos) * (cf - cf.Position)
end

local CARRY_BODY_NORTH_LOOK = Vector3.new(0, 0, -1)

local function getNorthSouthCarryCFrame(pos)
    return CFrame.lookAt(pos, pos + CARRY_BODY_NORTH_LOOK, Vector3.yAxis)
end

local function getNorthSouthGrabCFrame(pos)
    return CFrame.lookAt(pos, pos + CARRY_BODY_NORTH_LOOK, Vector3.yAxis)
end

local function placeCarriedBodyAtPosition(carriedHRP, pos, orientNorthSouth)
    if not (carriedHRP and pos) then
        return
    end
    if orientNorthSouth then
        carriedHRP.CFrame = getNorthSouthCarryCFrame(pos)
        return
    end
    carriedHRP.CFrame = cframeWithPosition(carriedHRP.CFrame, pos)
end

local function moveStandToCFrameExact(myChar, myHRP, cf)
    if not (myHRP and cf) then
        return
    end
    if myChar then
        myChar:PivotTo(cf)
    else
        myHRP.CFrame = cf
    end
    resetPartVelocity(myHRP)
end

local function getGrabTargetPart(targetChar)
    if not targetChar then
        return nil
    end
    return targetChar:FindFirstChild("UpperTorso")
        or targetChar:FindFirstChild("HumanoidRootPart")
        or targetChar:FindFirstChild("Torso")
        or targetChar:FindFirstChild("Head")
end

local function getGrabTargetParts(targetChar, preferredNames)
    if not targetChar then
        return {}
    end

    local parts = {}
    local seen = {}
    local function pushPart(part)
        if part and part.Parent and not seen[part] then
            seen[part] = true
            table.insert(parts, part)
        end
    end

    if preferredNames then
        for _, name in ipairs(preferredNames) do
            pushPart(targetChar:FindFirstChild(name))
        end
    end

    pushPart(getGrabTargetPart(targetChar))
    return parts
end

isNearPosition = function(part, position, maxDistance)
    if not (part and position) then
        return false
    end
    return (part.Position - position).Magnitude <= (maxDistance or 12)
end

local bringGrabLockUntil = 0
bringRunId = 0
bringAttemptTargetUserId = nil
bringAttemptDeliveryMode = false
local bringConnectionCharacter = nil
local bringConnectionRunId = nil

local function disconnectBringConnection()
    if bringconnection then
        bringconnection:Disconnect()
        bringconnection = nil
    end
    bringConnectionCharacter = nil
    bringConnectionRunId = nil
end

function resetBringGrabAttemptState()
    bringRunId = (bringRunId or 0) + 1
    bringGrabLockUntil = 0
    bringAttemptTargetUserId = nil
    bringAttemptDeliveryMode = false
    disconnectBringConnection()
end


local function getLiveCarryRoot(targetChar)
    if not targetChar then
        return nil
    end
    return targetChar:FindFirstChild("HumanoidRootPart")
        or targetChar:FindFirstChild("UpperTorso")
        or targetChar:FindFirstChild("Torso")
end

local function isLocalGrabLinkActive(targetChar)
    local myChar = LocalPlayer and LocalPlayer.Character
    if not (targetChar and myChar) then
        return false
    end

    local grabConstraint = targetChar:FindFirstChild("GRABBING_CONSTRAINT")
    return grabConstraint ~= nil and isConstraintLinkedToLocal(grabConstraint, myChar)
end

local function isCarryReleaseConfirmed(targetChar)
    if not targetChar or not targetChar.Parent then
        return true
    end

    local targetRoot = getLiveCarryRoot(targetChar)
    if not (targetRoot and targetRoot.Parent) then
        return true
    end

    return not isLocalGrabLinkActive(targetChar)
end

local function canSendGrabRemote()
    return os.clock() >= (bringGrabLockUntil or 0)
end

local function lockGrabRemoteWindow(duration)
    bringGrabLockUntil = os.clock() + math.max(duration or BRING_GRAB_LOCKOUT_TIME, 0.1)
end

isStrictlyAttachedToStand = function(targetChar, maxDistance)
    if not targetChar then
        return false
    end

    local grabConstraint = targetChar:FindFirstChild("GRABBING_CONSTRAINT")
    local myChar = LocalPlayer and LocalPlayer.Character
    if not (grabConstraint and myChar and isConstraintLinkedToLocal(grabConstraint, myChar)) then
        return false
    end

    local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
    local targetHRP = getLiveCarryRoot(targetChar)
    if not (myHRP and targetHRP) then
        return false
    end

    local allowedDistance = maxDistance or BRING_STRICT_ATTACH_DISTANCE
    local rootDistance = (targetHRP.Position - myHRP.Position).Magnitude
    return rootDistance <= allowedDistance
end

local function isCarryAttachedToStand(targetChar, maxDistance)
    return isStrictlyAttachedToStand(targetChar, maxDistance or FAST_BRING_ATTACH_CONFIRM_DISTANCE)
end

local function ensureCarryAttachedToStand(targetChar, loopCount, waitTime, maxDistance, orientNorthSouth)
    if not targetChar then
        return false
    end

    local loops = math.max(loopCount or FAST_BRING_ATTACH_CONFIRM_LOOPS, 1)
    local pauseTime = waitTime or FAST_BRING_ATTACH_CONFIRM_WAIT
    local myChar = LocalPlayer and LocalPlayer.Character
    local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
    local targetPart = getGrabTargetPart(targetChar)
    local targetHRP = getLiveCarryRoot(targetChar)
    if not (myHRP and targetPart and targetHRP) then
        return false
    end

    for _ = 1, loops do
        if isStrictlyAttachedToStand(targetChar, maxDistance or FAST_BRING_ATTACH_CONFIRM_DISTANCE) then
            return true
        end
        local holdPos = targetPart.Position + Vector3.new(0, 2.8, 0)
        local holdCFrame = orientNorthSouth and getNorthSouthGrabCFrame(holdPos) or CFrame.lookAt(holdPos, targetPart.Position)
        moveStandToCFrameExact(myChar, myHRP, holdCFrame)
        placeCarriedBodyAtPosition(targetHRP, myHRP.Position, orientNorthSouth and true or false)
        resetPartVelocity(targetHRP)
        task.wait(pauseTime)
    end

    return isStrictlyAttachedToStand(targetChar, maxDistance or FAST_BRING_ATTACH_CONFIRM_DISTANCE)
end

function confirmBringCarryWithRetry(targetChar, confirmGrab, orientNorthSouth, hardLockRounds, hardLockOffsets, hardLockSettle, hardLockRecheck, hardLockPartNames)
    if not (targetChar and confirmGrab) then
        return false
    end

    if confirmGrab() and ensureCarryAttachedToStand(
        targetChar,
        FAST_BRING_ATTACH_CONFIRM_LOOPS,
        FAST_BRING_ATTACH_CONFIRM_WAIT,
        FAST_BRING_ATTACH_CONFIRM_DISTANCE,
        orientNorthSouth
    ) then
        return true
    end

    task.wait(0.06)

    if confirmGrab() and ensureCarryAttachedToStand(
        targetChar,
        FAST_BRING_ATTACH_CONFIRM_LOOPS + 3,
        FAST_BRING_ATTACH_CONFIRM_WAIT,
        FAST_BRING_ATTACH_CONFIRM_DISTANCE + 1,
        orientNorthSouth
    ) then
        return true
    end

    local grabbed = attemptReliableBringGrab(targetChar, confirmGrab, hardLockRounds, {
        approachOffsets = hardLockOffsets,
        settleTime = hardLockSettle,
        recheckWait = hardLockRecheck,
        targetPartNames = hardLockPartNames,
        orientNorthSouth = orientNorthSouth,
    })

    if not grabbed then
        return false
    end

    return ensureCarryAttachedToStand(
        targetChar,
        FAST_BRING_ATTACH_CONFIRM_LOOPS + 3,
        FAST_BRING_ATTACH_CONFIRM_WAIT,
        FAST_BRING_ATTACH_CONFIRM_DISTANCE + 1,
        orientNorthSouth
    )
end

local function attemptReliableBringGrab(targetChar, confirmGrab, roundCount, options)
    if not (targetChar and confirmGrab) then
        return false
    end

    options = options or {}
    local myChar = LocalPlayer and LocalPlayer.Character
    local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
    if not myHRP then
        return false
    end

    local grabbed = confirmGrab()
    if grabbed then
        lockGrabRemoteWindow()
        return true
    end

    local rounds = math.max(roundCount or GRAB_RETRY_ROUNDS, 1)
    local approachOffsets = options.approachOffsets or GRAB_APPROACH_OFFSETS
    local settleTime = options.settleTime or GRAB_RETRY_SETTLE
    local recheckWait = options.recheckWait or GRAB_RECHECK_WAIT
    local targetPartNames = options.targetPartNames
    local orientNorthSouth = options.orientNorthSouth
    setNoclip(true)
    local ok, err = pcall(function()
        for _ = 1, rounds do
            if grabbed then
                break
            end
            local targetParts = getGrabTargetParts(targetChar, targetPartNames)
            if #targetParts == 0 then
                break
            end
            for _, targetPart in ipairs(targetParts) do
                if grabbed then
                    break
                end
                for _, offset in ipairs(approachOffsets) do
                    if grabbed then
                        break
                    end
                    if not (targetPart and targetPart.Parent) then
                        break
                    end
                    local approachPos = targetPart.Position + offset
                    local approachCFrame = orientNorthSouth and getNorthSouthGrabCFrame(approachPos) or CFrame.lookAt(approachPos, targetPart.Position)
                    moveStandToCFrameExact(myChar, myHRP, approachCFrame)
                    grabAttemptAt[targetChar] = os.clock()
                    local hasConstraintNow = targetChar:FindFirstChild("GRABBING_CONSTRAINT") ~= nil
                    if not hasConstraintNow and canSendGrabRemote() then
                        ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                    end
                    task.wait(settleTime)
                    grabbed = confirmGrab()
                    if grabbed then
                        lockGrabRemoteWindow()
                        local targetHRP = getLiveCarryRoot(targetChar)
                        if targetHRP then
                            placeCarriedBodyAtPosition(targetHRP, myHRP.Position, orientNorthSouth and true or false)
                            resetPartVelocity(targetHRP)
                        end
                        break
                    end
                end
            end
        end
    end)
    setNoclip(false)
    if not ok then
        warn(err)
    end

    if grabbed then
        return true
    end

    if targetChar:FindFirstChild("GRABBING_CONSTRAINT") then
        local targetHRP = getLiveCarryRoot(targetChar)
        if targetHRP and myHRP then
            placeCarriedBodyAtPosition(targetHRP, myHRP.Position, orientNorthSouth and true or false)
            resetPartVelocity(targetHRP)
        end
        task.wait(recheckWait)
        if confirmGrab() or ensureCarryAttachedToStand(targetChar, 6, 0.04, FAST_BRING_ATTACH_CONFIRM_DISTANCE + 1, orientNorthSouth) then
            lockGrabRemoteWindow()
            return true
        end
    end

    return false
end

local function releaseGrabReliably(confirmGrab, attemptCount, waitTime, options)
    options = options or {}
    local attempts = math.max(attemptCount or DROP_RELEASE_ATTEMPTS, 1)
    local pauseTime = waitTime or DROP_RELEASE_WAIT
    local lockout = options.lockout
    local releaseCheck = options.releaseCheck

    local function hasReleased()
        if type(releaseCheck) == "function" then
            local ok, released = pcall(releaseCheck)
            if ok then
                return released
            end
        end
        return not confirmGrab()
    end

    for _ = 1, attempts do
        if hasReleased() then
            return true
        end
        ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
        if lockout then
            lockGrabRemoteWindow(lockout)
        end
        task.wait(pauseTime)
    end

    return hasReleased()
end

function forceStrictDeliveryReleaseAtDestination(myChar, myHRP, carriedCharacter, carriedHRP, settleCFrame, releaseTargetPos, refreshSettleState)
    if not (myHRP and carriedCharacter and carriedHRP and settleCFrame and releaseTargetPos) then
        return false, settleCFrame, releaseTargetPos
    end

    local currentSettleCFrame = settleCFrame
    local currentReleaseTargetPos = releaseTargetPos

    for _ = 1, math.max(STRICT_DROP_FORCE_RELEASE_ATTEMPTS, 1) do
        if type(refreshSettleState) == "function" then
            local refreshedStandCFrame, refreshedReleaseTargetPos = refreshSettleState(currentSettleCFrame, currentReleaseTargetPos)
            if refreshedStandCFrame then
                currentSettleCFrame = refreshedStandCFrame
            end
            if refreshedReleaseTargetPos then
                currentReleaseTargetPos = refreshedReleaseTargetPos
            end
        end

        moveStandToCFrameExact(myChar, myHRP, currentSettleCFrame)
        placeCarriedBodyAtPosition(carriedHRP, currentReleaseTargetPos, true)
        resetPartVelocity(myHRP)
        resetPartVelocity(carriedHRP)

        for _ = 1, math.max(STRICT_DROP_FORCE_RELEASE_EXIT_LOOPS, 1) do
            ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
            task.wait(STRICT_DROP_FORCE_RELEASE_WAIT)

            if isCarryReleaseConfirmed(carriedCharacter)
                and isNearPosition(carriedHRP, currentReleaseTargetPos, STRICT_DROP_CARRIED_DISTANCE + 3) then
                return true, currentSettleCFrame, currentReleaseTargetPos
            end
        end

        local exitCFrame = getNorthSouthCarryCFrame(
            currentReleaseTargetPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, DROP_BACK_OFFSET.Z * 0.55)
        )

        for _ = 1, math.max(STRICT_DROP_FORCE_RELEASE_EXIT_LOOPS, 1) do
            moveStandToCFrameExact(myChar, myHRP, exitCFrame)
            ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
            task.wait(STRICT_DROP_FORCE_RELEASE_WAIT)

            if isCarryReleaseConfirmed(carriedCharacter)
                and isNearPosition(carriedHRP, currentReleaseTargetPos, STRICT_DROP_CARRIED_DISTANCE + 4) then
                return true, currentSettleCFrame, currentReleaseTargetPos
            end
        end

        moveStandToCFrameExact(myChar, myHRP, currentSettleCFrame)
        placeCarriedBodyAtPosition(carriedHRP, currentReleaseTargetPos, true)
        resetPartVelocity(myHRP)
        resetPartVelocity(carriedHRP)
        task.wait(STRICT_DROP_FORCE_RELEASE_WAIT)
    end

    return false, currentSettleCFrame, currentReleaseTargetPos
end

function invalidateToDeliveryRun()
    toDeliveryRunId = (toDeliveryRunId or 0) + 1
    return toDeliveryRunId
end

function runOwnerDeliveryCommand(runId)
    task.spawn(function()
        local function isActive()
            return toDeliveryActive
                and (toDeliveryRunId == runId)
                and not hardStop
        end

        local function resolveDropState()
            local baseCFrame, releasePos = resolveActiveDeliveryDropState()
            if baseCFrame then
                lastToDropCFrame = baseCFrame
            end
            return baseCFrame, releasePos
        end

        local function refreshSettleState(currentStandCFrame, currentReleaseTargetPos)
            local _, liveReleasePos = resolveDropState()
            local releasePos = liveReleasePos or currentReleaseTargetPos
            if not releasePos then
                return currentStandCFrame, currentReleaseTargetPos
            end
            return getNorthSouthGrabCFrame(releasePos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0)), releasePos
        end

        local function finishDeliverySuccess()
            if toDeliveryRunId ~= runId then
                return
            end

            lockedTarget = nil
            lockedTargetUserId = nil
            autoLocked = false
            bringonly = false
            teleporting = false
            gotoCFrame = nil
            gotoTarget = nil
            gotoTargetUserId = nil
            pendingGotoTarget = nil
            pendingGotoTargetUserId = nil
            forceBringDrop = false
            lastToDestination = nil
            toDeliveryActive = false
            lastToDropCFrame = nil
            commandSender = nil
            skyTarget = nil
            savedTarget5 = nil

            local resumedTask = restoreDeliveryResumeState()
            if not resumedTask then
                if not autosaveActive and not isCurrentlyGrabbing() then
                    if not resumeOwnerFollow() then
                        voiding = true
                    else
                        voiding = false
                    end
                end
            end

            resetBringGrabAttemptState()
            requestPostCarryCombatRecovery(lockedTarget or sentrytarget, true)
            reloadTool()
        end

        while isActive() do
            local ownerPlr = Players:FindFirstChild(Owner)
            local ownerChar = ownerPlr and ownerPlr.Character
            local myChar = LocalPlayer.Character
            local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
            local ownerHum = ownerChar and ownerChar:FindFirstChildOfClass("Humanoid")
            local ownerRoot = getLiveCarryRoot(ownerChar)

            if not (ownerPlr and ownerChar and myChar and myHRP and ownerHum and ownerRoot) then
                task.wait(0.05)
                continue
            end

            commandSender = Owner
            voiding = false
            bringonly = false

            local function confirmOwnerGrabSoft()
                return isHoldingTarget(ownerChar)
            end
            local function confirmOwnerGrab()
                return isHoldingTargetForDelivery(ownerChar)
            end

            local ownerCarryAttached = confirmOwnerGrab()
            if not ownerCarryAttached and confirmOwnerGrabSoft() then
                ownerCarryAttached = ensureCarryAttachedToStand(
                    ownerChar,
                    AUTOSAVE_ATTACH_CONFIRM_LOOPS,
                    AUTOSAVE_ATTACH_CONFIRM_WAIT,
                    AUTOSAVE_ATTACH_CONFIRM_DISTANCE,
                    false
                )
            end

            if ownerCarryAttached then
                lockedTarget = nil
                lockedTargetUserId = nil
                autoLocked = false
                teleporting = false
                local delivered = false
                withNoclip(function()
                    local carriedHRP = getLiveCarryRoot(ownerChar)
                    if not (carriedHRP and confirmOwnerGrab()) then
                        return
                    end

                    local _, releaseTargetPos = resolveDropState()
                    if not releaseTargetPos then
                        return
                    end

                    local hoverCFrame = getNorthSouthGrabCFrame(releaseTargetPos + Vector3.new(0, FAST_BRING_HOVER_HEIGHT, 0))
                    local settleCFrame = getNorthSouthGrabCFrame(releaseTargetPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0))

                    moveStandToCFrameExact(myChar, myHRP, hoverCFrame)
                    resetPartVelocity(myHRP)
                    placeCarriedBodyAtPosition(carriedHRP, myHRP.Position, true)
                    resetPartVelocity(carriedHRP)

                    local standArrived, carriedArrived, refreshedStandCFrame, refreshedReleaseTargetPos = alignCarryDropPosition(
                        myChar,
                        myHRP,
                        carriedHRP,
                        settleCFrame,
                        releaseTargetPos,
                        DROP_SYNC_TIMEOUT,
                        STRICT_DROP_STAND_DISTANCE,
                        STRICT_DROP_CARRIED_DISTANCE,
                        refreshSettleState,
                        true
                    )
                    if refreshedStandCFrame then
                        settleCFrame = refreshedStandCFrame
                    end
                    if refreshedReleaseTargetPos then
                        releaseTargetPos = refreshedReleaseTargetPos
                    end

                    if not (standArrived and carriedArrived and confirmOwnerGrab()) then
                        return
                    end

                    local pinStandArrived, pinCarriedArrived, pinnedStandCFrame, pinnedReleaseTargetPos = pinCarryDropPosition(
                        myChar,
                        myHRP,
                        carriedHRP,
                        settleCFrame,
                        releaseTargetPos,
                        FAST_BRING_PIN_LOOPS + 4,
                        FAST_BRING_PIN_WAIT,
                        STRICT_DROP_STAND_DISTANCE,
                        STRICT_DROP_CARRIED_DISTANCE,
                        confirmOwnerGrab,
                        refreshSettleState,
                        true
                    )
                    if pinnedStandCFrame then
                        settleCFrame = pinnedStandCFrame
                    end
                    if pinnedReleaseTargetPos then
                        releaseTargetPos = pinnedReleaseTargetPos
                    end

                    if not (pinStandArrived and pinCarriedArrived and confirmOwnerGrab()) then
                        return
                    end

                    moveStandToCFrameExact(myChar, myHRP, settleCFrame)
                    placeCarriedBodyAtPosition(carriedHRP, releaseTargetPos, true)
                    resetPartVelocity(myHRP)
                    resetPartVelocity(carriedHRP)
                    task.wait(0.04)

                    local strictReady = isStrictDeliveryReadyForRelease(
                        myHRP,
                        carriedHRP,
                        ownerChar,
                        STRICT_DROP_STAND_DISTANCE,
                        STRICT_DROP_CARRIED_DISTANCE
                    )
                    if not strictReady then
                        return
                    end

                    local released = releaseGrabReliably(
                        confirmOwnerGrab,
                        DROP_RELEASE_ATTEMPTS + 4,
                        DROP_RELEASE_WAIT,
                        {
                            releaseCheck = function()
                                return isCarryReleaseConfirmed(ownerChar)
                            end,
                        }
                    )

                    if not released then
                        local forcedReleased, forcedSettleCFrame, forcedReleaseTargetPos = forceStrictDeliveryReleaseAtDestination(
                            myChar,
                            myHRP,
                            ownerChar,
                            carriedHRP,
                            settleCFrame,
                            releaseTargetPos,
                            refreshSettleState
                        )
                        if forcedSettleCFrame then
                            settleCFrame = forcedSettleCFrame
                        end
                        if forcedReleaseTargetPos then
                            releaseTargetPos = forcedReleaseTargetPos
                        end
                        released = forcedReleased
                    end

                    if not released then
                        return
                    end

                    local exitCFrame = getNorthSouthCarryCFrame(
                        releaseTargetPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, DROP_BACK_OFFSET.Z * 0.55)
                    )
                    moveStandToCFrameExact(myChar, myHRP, exitCFrame)
                    resetPartVelocity(myHRP)
                    task.wait(0.05)

                    delivered = isCarryReleaseConfirmed(ownerChar)
                        and isNearPosition(carriedHRP, releaseTargetPos, STRICT_DROP_CARRIED_DISTANCE + 4)
                end)

                if delivered then
                    finishDeliverySuccess()
                    return
                end

                task.wait(0.05)
                continue
            end

            local bodyEffects = ownerChar:FindFirstChild("BodyEffects")
            local ownerKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
            local ownerTargetPart = getGrabTargetPart(ownerChar) or ownerRoot

            if ownerKO then
                lockedTarget = nil
                lockedTargetUserId = nil
                autoLocked = false
                teleporting = false
                local grabbed = attemptReliableBringGrab(ownerChar, confirmOwnerGrabSoft, AUTOSAVE_GRAB_ROUNDS, {
                    approachOffsets = AUTOSAVE_GRAB_APPROACH_OFFSETS,
                    settleTime = 0.04,
                    recheckWait = 0.08,
                    targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                })

                if not grabbed then
                    local autosaveLockParts = getGrabTargetParts(ownerChar, DELIVERY_OWNER_GRAB_PART_NAMES)
                    local autosaveLockPart = autosaveLockParts[1] or ownerTargetPart
                    if autosaveLockPart and autosaveLockPart.Parent then
                        local lockOffset = AUTOSAVE_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 2.0, 0)
                        local lockPos = autosaveLockPart.Position + lockOffset
                        moveStandToCFrameExact(myChar, myHRP, CFrame.lookAt(lockPos, autosaveLockPart.Position))
                        task.wait(0.03)
                    end
                    grabbed = attemptReliableBringGrab(ownerChar, confirmOwnerGrabSoft, AUTOSAVE_GRAB_HARDLOCK_ROUNDS, {
                        approachOffsets = AUTOSAVE_GRAB_HARDLOCK_OFFSETS,
                        settleTime = 0.05,
                        recheckWait = 0.1,
                        targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                    })
                end

                if grabbed and not ensureCarryAttachedToStand(
                    ownerChar,
                    AUTOSAVE_ATTACH_CONFIRM_LOOPS,
                    AUTOSAVE_ATTACH_CONFIRM_WAIT,
                    AUTOSAVE_ATTACH_CONFIRM_DISTANCE,
                    false
                ) then
                    grabbed = false
                    local autosaveLockParts = getGrabTargetParts(ownerChar, DELIVERY_OWNER_GRAB_PART_NAMES)
                    local autosaveLockPart = autosaveLockParts[1] or ownerTargetPart
                    if autosaveLockPart and autosaveLockPart.Parent then
                        local lockOffset = AUTOSAVE_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 2.0, 0)
                        local lockPos = autosaveLockPart.Position + lockOffset
                        moveStandToCFrameExact(myChar, myHRP, CFrame.lookAt(lockPos, autosaveLockPart.Position))
                        task.wait(0.03)
                    end
                    grabbed = attemptReliableBringGrab(ownerChar, confirmOwnerGrabSoft, AUTOSAVE_GRAB_HARDLOCK_ROUNDS, {
                        approachOffsets = AUTOSAVE_GRAB_HARDLOCK_OFFSETS,
                        settleTime = 0.05,
                        recheckWait = 0.1,
                        targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                    })
                end

                if grabbed and ensureCarryAttachedToStand(
                    ownerChar,
                    AUTOSAVE_ATTACH_CONFIRM_LOOPS,
                    AUTOSAVE_ATTACH_CONFIRM_WAIT,
                    AUTOSAVE_ATTACH_CONFIRM_DISTANCE,
                    false
                ) then
                    lockGrabRemoteWindow()
                end
            else
                lockedTarget = ownerPlr
                lockedTargetUserId = ownerPlr.UserId
                autoLocked = false
                teleporting = true
                if ownerTargetPart and ownerTargetPart.Parent then
                    local approachOffset = DELIVERY_OWNER_GRAB_APPROACH_OFFSETS[1] or Vector3.new(0, 2.8, 0)
                    moveStandToCFrameExact(myChar, myHRP, getNorthSouthGrabCFrame(ownerTargetPart.Position + approachOffset))
                    resetPartVelocity(myHRP)
                end
                tryForceBringKO(ownerPlr, 0)
            end

            task.wait(0.06)
        end
    end)
end

local function alignCarryDropPosition(myChar, myHRP, carriedHRP, dropCFrame, releaseTargetPos, timeout, standDistance, carriedDistance, refreshDropState, orientNorthSouth)
    if not (myHRP and dropCFrame and releaseTargetPos) then
        return false, carriedHRP == nil, dropCFrame, releaseTargetPos
    end

    local deadline = os.clock() + math.max(timeout or DROP_SYNC_TIMEOUT, 0.2)
    local standRadius = standDistance or 12
    local carriedRadius = carriedDistance or 14
    local standArrived = false
    local carriedArrived = carriedHRP == nil
    local currentDropCFrame = dropCFrame
    local currentReleaseTargetPos = releaseTargetPos

    repeat
        if type(refreshDropState) == "function" then
            local refreshedDropCFrame, refreshedReleaseTargetPos = refreshDropState(currentDropCFrame, currentReleaseTargetPos)
            if refreshedDropCFrame then
                currentDropCFrame = refreshedDropCFrame
            end
            if refreshedReleaseTargetPos then
                currentReleaseTargetPos = refreshedReleaseTargetPos
            end
        end

        moveStandToCFrameExact(myChar, myHRP, currentDropCFrame)
        standArrived = isNearPosition(myHRP, currentReleaseTargetPos, standRadius)

        if carriedHRP then
            placeCarriedBodyAtPosition(carriedHRP, currentReleaseTargetPos, orientNorthSouth)
            resetPartVelocity(carriedHRP)
            carriedArrived = isNearPosition(carriedHRP, currentReleaseTargetPos, carriedRadius)
        end

        if standArrived and carriedArrived then
            return true, true, currentDropCFrame, currentReleaseTargetPos
        end

        task.wait(0.04)
    until os.clock() >= deadline

    return standArrived, carriedArrived, currentDropCFrame, currentReleaseTargetPos
end

local function pinCarryDropPosition(myChar, myHRP, carriedHRP, standCFrame, releaseTargetPos, loopCount, waitTime, standDistance, carriedDistance, confirmGrab, refreshDropState, orientNorthSouth)
    if not (standCFrame and releaseTargetPos) then
        return false, carriedHRP == nil, standCFrame, releaseTargetPos
    end

    local loops = math.max(loopCount or FAST_BRING_PIN_LOOPS, 1)
    local pauseTime = waitTime or FAST_BRING_PIN_WAIT
    local currentStandCFrame = standCFrame
    local currentReleaseTargetPos = releaseTargetPos
    local standPinned = false
    local carriedPinned = carriedHRP == nil

    for _ = 1, loops do
        if type(confirmGrab) == "function" and not confirmGrab() then
            break
        end

        if type(refreshDropState) == "function" then
            local refreshedStandCFrame, refreshedReleaseTargetPos = refreshDropState(currentStandCFrame, currentReleaseTargetPos)
            if refreshedStandCFrame then
                currentStandCFrame = refreshedStandCFrame
            end
            if refreshedReleaseTargetPos then
                currentReleaseTargetPos = refreshedReleaseTargetPos
            end
        end

        if myHRP and currentStandCFrame then
            moveStandToCFrameExact(myChar, myHRP, currentStandCFrame)
            resetPartVelocity(myHRP)
        end

        standPinned = myHRP and isNearPosition(myHRP, currentReleaseTargetPos, standDistance or FAST_BRING_STAND_DISTANCE) or false

        if carriedHRP and currentReleaseTargetPos then
            placeCarriedBodyAtPosition(carriedHRP, currentReleaseTargetPos, orientNorthSouth)
            resetPartVelocity(carriedHRP)
            carriedPinned = isNearPosition(carriedHRP, currentReleaseTargetPos, carriedDistance or FAST_BRING_PIN_DISTANCE)
        else
            carriedPinned = true
        end

        if standPinned and carriedPinned then
            return true, true, currentStandCFrame, currentReleaseTargetPos
        end

        task.wait(pauseTime)
    end

    return standPinned, carriedPinned, currentStandCFrame, currentReleaseTargetPos
end

local function stabilizeReleasedCarryAtPlayer(myChar, myHRP, carriedHRP, targetPlayer, loopCount, waitTime, requiredHits, maxDistance, standHeight, orientNorthSouth)
    if not (carriedHRP and targetPlayer) then
        return false, nil
    end

    local loops = math.max(loopCount or OWNER_BRING_POST_RELEASE_PIN_LOOPS, 1)
    local pauseTime = waitTime or OWNER_BRING_POST_RELEASE_PIN_WAIT
    local neededHits = math.max(requiredHits or OWNER_BRING_POST_RELEASE_REQUIRED_HITS, 1)
    local allowedDistance = maxDistance or OWNER_BRING_FINAL_TARGET_DISTANCE
    local settleHeight = standHeight or FAST_BRING_SETTLE_HEIGHT
    local stableHits = 0
    local lastLivePos = nil

    for _ = 1, loops do
        local _, liveOwnerPos = getPlayerDestinationCFrame(targetPlayer)
        if not liveOwnerPos then
            break
        end
        lastLivePos = liveOwnerPos

        if myHRP then
            moveStandToCFrameExact(myChar, myHRP, CFrame.new(liveOwnerPos + Vector3.new(0, settleHeight, 0)))
            resetPartVelocity(myHRP)
        end

        placeCarriedBodyAtPosition(carriedHRP, liveOwnerPos, orientNorthSouth)
        resetPartVelocity(carriedHRP)

        if isNearPosition(carriedHRP, liveOwnerPos, allowedDistance) then
            stableHits += 1
            if stableHits >= neededHits then
                return true, liveOwnerPos
            end
        else
            stableHits = 0
        end

        task.wait(pauseTime)
    end

    return lastLivePos and isNearPosition(carriedHRP, lastLivePos, allowedDistance) or false, lastLivePos
end

local function deliverCarriedTargetToOwnerDirectly(myChar, myHRP, carriedCharacter, targetPlayer, confirmGrab, orientNorthSouth)
    if not (myHRP and carriedCharacter and targetPlayer and confirmGrab) then
        return false
    end

    local carriedHRP = carriedCharacter:FindFirstChild("HumanoidRootPart")
        or carriedCharacter:FindFirstChild("UpperTorso")
        or carriedCharacter:FindFirstChild("Torso")
    local carriedHum = carriedCharacter:FindFirstChildOfClass("Humanoid")
    if not carriedHRP then
        return false
    end

    if carriedHum then
        pcall(function()
            carriedHum:ChangeState(Enum.HumanoidStateType.Physics)
        end)
        carriedHum.PlatformStand = true
    end

    local function pinToOwner(loopCount, waitTime, requireGrab)
        local loops = math.max(loopCount or OWNER_BRING_PRE_RELEASE_PIN_LOOPS, 1)
        local pauseTime = waitTime or OWNER_BRING_PRE_RELEASE_PIN_WAIT
        local stableHits = 0
        local lastLivePos = nil

        for _ = 1, loops do
            if requireGrab and not confirmGrab() then
                break
            end

            local _, liveOwnerPos = getPlayerDestinationCFrame(targetPlayer)
            if not liveOwnerPos then
                break
            end
            lastLivePos = liveOwnerPos

            moveStandToCFrameExact(myChar, myHRP, CFrame.new(liveOwnerPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0)))
            resetPartVelocity(myHRP)
            placeCarriedBodyAtPosition(carriedHRP, liveOwnerPos, orientNorthSouth)
            resetPartVelocity(carriedHRP)

            if requireGrab and not isStrictlyAttachedToStand(carriedCharacter, BRING_STRICT_ATTACH_DISTANCE) then
                stableHits = 0
                task.wait(pauseTime)
                continue
            end

            if isNearPosition(carriedHRP, liveOwnerPos, OWNER_BRING_FINAL_TARGET_DISTANCE) then
                stableHits += 1
                if stableHits >= OWNER_BRING_POST_RELEASE_REQUIRED_HITS then
                    return true, liveOwnerPos
                end
            else
                stableHits = 0
            end

            task.wait(pauseTime)
        end

        return lastLivePos and isNearPosition(carriedHRP, lastLivePos, OWNER_BRING_FINAL_TARGET_DISTANCE) or false, lastLivePos
    end

    local pinnedBeforeRelease = pinToOwner(OWNER_BRING_PRE_RELEASE_PIN_LOOPS, OWNER_BRING_PRE_RELEASE_PIN_WAIT, true)
    if not pinnedBeforeRelease then
        if carriedHum then
            carriedHum.PlatformStand = false
        end
        return false
    end

    local released = false
    for releaseAttempt = 1, math.max(OWNER_BRING_DIRECT_RELEASE_RETRIES, 1) do
        released = releaseGrabReliably(confirmGrab, DROP_RELEASE_ATTEMPTS, DROP_RELEASE_WAIT, {
            releaseCheck = function()
                return isCarryReleaseConfirmed(carriedCharacter)
            end,
        })
        if released then
            break
        end

        local repinned = pinToOwner(
            OWNER_BRING_DIRECT_REPIN_LOOPS,
            OWNER_BRING_DIRECT_REPIN_WAIT,
            true
        )
        if not repinned then
            break
        end

        task.wait(0.02 * releaseAttempt)
    end
    if not released then
        local settledWithoutRelease, liveOwnerPos = pinToOwner(
            OWNER_BRING_DIRECT_REPIN_LOOPS,
            OWNER_BRING_DIRECT_REPIN_WAIT,
            false
        )
        if settledWithoutRelease and isCarryReleaseConfirmed(carriedCharacter) then
            released = true
        elseif settledWithoutRelease then
            logDrop("owner direct handoff stayed linked after release retries; keeping hold for retry")
        elseif liveOwnerPos then
            logDrop(("owner direct handoff release retries ended at %.2f, %.2f, %.2f instead of owner %.2f, %.2f, %.2f"):format(
                carriedHRP.Position.X,
                carriedHRP.Position.Y,
                carriedHRP.Position.Z,
                liveOwnerPos.X,
                liveOwnerPos.Y,
                liveOwnerPos.Z
            ))
        end
        if not released then
            if carriedHum then
                carriedHum.PlatformStand = false
            end
            return false
        end
    end

    local pinnedAfterRelease, liveOwnerPos = pinToOwner(OWNER_BRING_POST_RELEASE_PIN_LOOPS, OWNER_BRING_POST_RELEASE_PIN_WAIT, false)

    if carriedHum then
        carriedHum.PlatformStand = false
        pcall(function()
            carriedHum:ChangeState(Enum.HumanoidStateType.GettingUp)
        end)
    end

    if not pinnedAfterRelease and liveOwnerPos then
        logDrop(("owner direct handoff target ended at %.2f, %.2f, %.2f instead of owner %.2f, %.2f, %.2f"):format(
            carriedHRP.Position.X,
            carriedHRP.Position.Y,
            carriedHRP.Position.Z,
            liveOwnerPos.X,
            liveOwnerPos.Y,
            liveOwnerPos.Z
        ))
    end

    return pinnedAfterRelease
end

local function clampOwnerAboveTarget(myChar, myHRP, ownerHRP, targetY)
    if not (ownerHRP and targetY) then
        return
    end
    local delta = ownerHRP.Position.Y - targetY
    if delta <= 0 then
        return
    end
    local baseCFrame = (myChar and myChar:GetPivot()) or (myHRP and myHRP.CFrame)
    if not baseCFrame then
        return
    end
    local newPos = baseCFrame.Position - Vector3.new(0, delta, 0)
    local adjusted = cframeWithPosition(baseCFrame, newPos)
    if myChar then
        myChar:PivotTo(adjusted)
    elseif myHRP then
        myHRP.CFrame = adjusted
    end
    if myHRP then
        resetPartVelocity(myHRP)
    end
end

local function isHoldingTarget(targetChar)
    if not targetChar then
        return false
    end
    local grabConstraint = targetChar:FindFirstChild("GRABBING_CONSTRAINT")
    if not grabConstraint then
        grabSeenAt[targetChar] = nil
        return false
    end
    local myChar = game.Players.LocalPlayer.Character
    if not myChar then
        return false
    end
    if isConstraintLinkedToLocal(grabConstraint, myChar) then
        grabSeenAt[targetChar] = nil
        grabAttemptAt[targetChar] = nil
        return true
    end
    local myHRP = myChar:FindFirstChild("HumanoidRootPart")
    local targetPart = targetChar:FindFirstChild("HumanoidRootPart") or targetChar:FindFirstChild("UpperTorso")
    if not (myHRP and targetPart) then
        return false
    end
    if (targetPart.Position - myHRP.Position).Magnitude <= GRAB_CONFIRM_DISTANCE then
        grabSeenAt[targetChar] = nil
        grabAttemptAt[targetChar] = nil
        return true
    end

    local attemptAt = grabAttemptAt[targetChar]
    if attemptAt and (os.clock() - attemptAt) <= GRAB_FALLBACK_WINDOW then
        local bodyEffects = targetChar:FindFirstChild("BodyEffects")
        local koValue = bodyEffects and bodyEffects:FindFirstChild("K.O")
        if koValue and koValue.Value then
            if (targetPart.Position - myHRP.Position).Magnitude <= GRAB_FALLBACK_DISTANCE then
                grabSeenAt[targetChar] = nil
                grabAttemptAt[targetChar] = nil
                return true
            end
        end
    end

    local seenAt = grabSeenAt[targetChar]
    if not seenAt then
        grabSeenAt[targetChar] = os.clock()
        return false
    end
    if (os.clock() - seenAt) >= GRAB_CONFIRM_TIME then
        return true
    end
    return false
end

local function isHoldingTargetForDelivery(targetChar)
    return isStrictlyAttachedToStand(targetChar, BRING_STRICT_ATTACH_DISTANCE)
end

Players = game:GetService("Players")
LocalPlayer = Players.LocalPlayer
character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
TeleportService = game:GetService("TeleportService")

LocalPlayer.CharacterAdded:Connect(function(newCharacter)
    character = newCharacter
    character:WaitForChild("Humanoid")
end)

function equipTool(toolName)
    local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(toolName)
    if not tool then
        tool = game.Players.LocalPlayer:FindFirstChild(toolName)
    end
    local character = game.Players.LocalPlayer.Character
    if tool and character then
        tool.Parent = character
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid and tool.Parent ~= character then
            humanoid:EquipTool(tool)
        end
    end
end

whitelistedUsers = {}
activeListeners = {}
playerChatConnections = {}
recentMirroredChatMessages = {}
chatDispatchConnections = {}

TextChatService = game:GetService("TextChatService")

function isAuthorized(player)
    return player.Name == Owner or whitelistedUsers[player.Name]
end

function isProtected(player)
    return false
end

function removeOldListeners()
    for userId in pairs(activeListeners) do
        activeListeners[userId] = nil
    end
    for userId, connection in pairs(playerChatConnections) do
        if connection then
            connection:Disconnect()
        end
        playerChatConnections[userId] = nil
    end
end

local function disconnectPlayerChatRelay(userId)
    local connection = playerChatConnections[userId]
    if connection then
        connection:Disconnect()
        playerChatConnections[userId] = nil
    end
end

local function getIncomingChatSender(msg)
    local textSource = msg and msg.TextSource
    local userId = textSource and textSource.UserId
    if not userId then
        return nil
    end
    return Players:GetPlayerByUserId(userId)
end

local function buildLegacyChatDispatchMessage(payload)
    if type(payload) ~= "table" then
        return nil
    end

    local text = payload.Message or payload.message or payload.Text or payload.text
    if text == nil then
        return nil
    end

    local userId = payload.SpeakerUserId or payload.UserId
    if not userId then
        local speakerName = payload.FromSpeaker or payload.Speaker or payload.From
        local speaker = speakerName and Players:FindFirstChild(speakerName)
        userId = speaker and speaker.UserId
    end

    if not userId then
        return nil
    end

    return {
        Text = tostring(text),
        TextSource = {
            UserId = userId,
        },
    }
end

local function shouldSkipMirroredChat(senderUserId, text, sourceKind)
    if not senderUserId or text == nil then
        return false
    end

    local key = tostring(senderUserId) .. "\0" .. tostring(text)
    local now = os.clock()
    local previous = recentMirroredChatMessages[key]
    recentMirroredChatMessages[key] = {
        source = sourceKind,
        time = now,
    }

    return previous ~= nil
        and previous.source ~= sourceKind
        and (now - previous.time) <= 2
end

local function dispatchAuthorizedChatMessage(msg, sourceKind)
    local sender = getIncomingChatSender(msg)
    if not sender then
        return
    end

    local text = tostring(msg.Text or "")
    if text == "" then
        return
    end

    if shouldSkipMirroredChat(sender.UserId, text, sourceKind or "textchat") then
        return
    end

    local lower = text:lower()
    local isV = (lower == ".v") or lower:match("^%.v%s+")
    if isV then
        local ownerPlr = Players:FindFirstChild(Owner)
        local ownerId = ownerPlr and ownerPlr.UserId
        if sender.Name == Owner or (ownerId and sender.UserId == ownerId) then
            handleHideCommand()
        end
    end

    local handler = activeListeners[sender.UserId]
    if handler then
        task.spawn(handler, msg)
    end
end

local function disconnectChatDispatchConnection(key)
    local connection = chatDispatchConnections[key]
    if connection then
        connection:Disconnect()
        chatDispatchConnections[key] = nil
    end
end

local function setIncomingMessageFallback(enabled)
    if enabled then
        TextChatService.OnIncomingMessage = function(msg)
            dispatchAuthorizedChatMessage(msg, "textchat")
        end
    else
        TextChatService.OnIncomingMessage = nil
    end
end

local function connectFastChatDispatch()
    disconnectChatDispatchConnection("service")
    disconnectChatDispatchConnection("channel")
    disconnectChatDispatchConnection("channelsChild")
    disconnectChatDispatchConnection("serviceChild")
    disconnectChatDispatchConnection("legacy")
    disconnectChatDispatchConnection("legacyChild")

    local hasFastDispatch = false

    if TextChatService.MessageReceived then
        chatDispatchConnections.service = TextChatService.MessageReceived:Connect(function(msg)
            dispatchAuthorizedChatMessage(msg, "service")
        end)
        hasFastDispatch = true
    end

    local textChannels = TextChatService:FindFirstChild("TextChannels")
    if textChannels then
        local generalChannel = textChannels:FindFirstChild("RBXGeneral")
        if generalChannel and generalChannel.MessageReceived then
            textChannel = generalChannel
            chatDispatchConnections.channel = generalChannel.MessageReceived:Connect(function(msg)
                dispatchAuthorizedChatMessage(msg, "channel")
            end)
            hasFastDispatch = true
        end

        chatDispatchConnections.channelsChild = textChannels.ChildAdded:Connect(function(child)
            if child.Name == "RBXGeneral" then
                task.defer(connectFastChatDispatch)
            end
        end)
    else
        chatDispatchConnections.serviceChild = TextChatService.ChildAdded:Connect(function(child)
            if child.Name == "TextChannels" then
                task.defer(connectFastChatDispatch)
            end
        end)
    end

    local legacyEvents = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents")
    if legacyEvents then
        local filteredEvent = legacyEvents:FindFirstChild("OnMessageDoneFiltering")
        if filteredEvent and filteredEvent.OnClientEvent then
            chatDispatchConnections.legacy = filteredEvent.OnClientEvent:Connect(function(payload)
                local legacyMessage = buildLegacyChatDispatchMessage(payload)
                if legacyMessage then
                    dispatchAuthorizedChatMessage(legacyMessage, "legacy")
                end
            end)
            hasFastDispatch = true
        end

        chatDispatchConnections.legacyChild = legacyEvents.ChildAdded:Connect(function(child)
            if child.Name == "OnMessageDoneFiltering" then
                task.defer(connectFastChatDispatch)
            end
        end)
    else
        chatDispatchConnections.legacyChild = ReplicatedStorage.ChildAdded:Connect(function(child)
            if child.Name == "DefaultChatSystemChatEvents" then
                task.defer(connectFastChatDispatch)
            end
        end)
    end

    setIncomingMessageFallback(not hasFastDispatch)
end

benxActive = false
TweenService = game:GetService("TweenService")

function startBenx(targetPlayer)
    if not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then return end
    lockedTarget = nil
    voiding = false
    benxActive = true

    local tweenInfo = TweenInfo.new(0.2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)

    task.spawn(function()
        while benxActive do
            local char = LocalPlayer.Character
            local targetChar = targetPlayer.Character

            if char and char:FindFirstChild("HumanoidRootPart") and targetChar and targetChar:FindFirstChild("HumanoidRootPart") then
                local hrp = char.HumanoidRootPart
                local targetHRP = targetChar.HumanoidRootPart

                local frontPos = targetHRP.CFrame * CFrame.new(0, 0, -1)
                local backPos = targetHRP.CFrame * CFrame.new(0, 0, -4)

                local tween1 = TweenService:Create(hrp, tweenInfo, {CFrame = frontPos})
                tween1:Play()
                tween1.Completed:Wait()

                local tween2 = TweenService:Create(hrp, tweenInfo, {CFrame = backPos})
                tween2:Play()
                tween2.Completed:Wait()
            end
            if not benxActive then break end
        end
    end)
end

function updateDisplayName(player)
    return
end

function setupDisplayNameListener(player)
    if player.Character then
        updateDisplayName(player)
    end

    player.CharacterAdded:Connect(function()
        task.wait(0.1)
        updateDisplayName(player)
    end)
end

local function cancelAttackModes()
    invalidateToDeliveryRun()
    -- cancel any combat/loop targets
    ragebottargets = {}
    shouldSwitch = false
    currentTargetIndex = 1
    cancelSmiteCommandState()

    -- clear all targeting + relock state
    lockedTarget = nil
    lockedTargetUserId = nil
    autoLocked = false
    summonTarget = nil
    flameModeActive = false
    flameModeTargetUserId = nil
    flameModeTargetName = nil

    -- disable ALL mode flags
    stomponly = false
    bringonly = false
    takeonly = false
    getgenv().downonly = false
    opkill = false
    flingonly = false
    killall = false

    -- stop movement tasks tied to combat
    teleporting = false
    gotoPlayer = nil
    gotoCFrame = nil
    gotoTarget = nil
    gotoTargetUserId = nil
    pendingGotoTarget = nil
    pendingGotoTargetUserId = nil
    vehicleMode = false
    vehicleModel = nil
    forceBringDrop = false
    commandSender = nil
    toDeliveryActive = false
    lastToDestination = nil
    lastToDropCFrame = nil
    resetBringGrabAttemptState()
    clearDeliveryResumeState()
end

local function normalizePlayerInput(raw)
    raw = trimInput(raw)
    if not raw or raw == "" then
        return nil
    end
    -- Support `.assist "name"` / `.assist 'name'`
    for _ = 1, 2 do
        raw = raw:gsub("^%s*['\"]", ""):gsub("['\"]%s*$", "")
    end
    raw = trimInput(raw)
    if raw == "" then
        return nil
    end
    return raw
end

local function findPlayerByExactOrPartial(raw)
    local normalized = normalizePlayerInput(raw)
    if not normalized then
        return nil
    end
    local lowerInput = normalized:lower()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Name:lower() == lowerInput or plr.DisplayName:lower() == lowerInput then
            return plr
        end
    end
    return findPlayerByPartial(normalized)
end

local function resolveBringCommandTarget(rawInput)
    local parsed = normalizePlayerInput(rawInput)
    if not parsed then
        return nil, nil
    end

    local target = resolveDeliveryTargetPlayer(parsed) or findPlayerByPartial(parsed)
    if target == LocalPlayer or (target and target.Name == Owner) then
        return nil, parsed
    end

    return target, parsed
end

local function findPlayerByUserIdLocal(userId)
    if not userId then
        return nil
    end
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.UserId == userId then
            return plr
        end
    end
    return nil
end

local bindSentryAssistPlayer
local unbindSentryAssistPlayer

local function rememberSentryProtectedPlayer(player)
    if not player then
        return
    end
    getgenv().sentryprotected[player.Name] = true
    getgenv().sentryprotectedUsers[player.UserId] = player.Name
    if getgenv().lastHealths then
        local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
        getgenv().lastHealths[player.Name] = humanoid and humanoid.Health or nil
    end
    if bindSentryAssistPlayer then
        bindSentryAssistPlayer(player)
    end
end

local function forgetSentryProtectedName(raw)
    local normalized = normalizePlayerInput(raw)
    if not normalized then
        return false
    end

    local lowerInput = normalized:lower()
    local removed = false
    local removedUserIds = {}

    for storedName in pairs(getgenv().sentryprotected) do
        if tostring(storedName):lower() == lowerInput then
            getgenv().sentryprotected[storedName] = nil
            removed = true
        end
    end

    for userId, storedName in pairs(getgenv().sentryprotectedUsers) do
        if tostring(storedName or ""):lower() == lowerInput then
            getgenv().sentryprotectedUsers[userId] = nil
            table.insert(removedUserIds, userId)
            removed = true
        end
    end

    if getgenv().lastHealths then
        for storedName in pairs(getgenv().lastHealths) do
            if tostring(storedName):lower() == lowerInput then
                getgenv().lastHealths[storedName] = nil
                removed = true
            end
        end
    end

    if unbindSentryAssistPlayer then
        for _, userId in ipairs(removedUserIds) do
            unbindSentryAssistPlayer(userId)
        end
    end

    return removed
end

local function forgetSentryProtectedPlayer(player)
    if not player then
        return false
    end
    local removed = forgetSentryProtectedName(player.Name)
    getgenv().sentryprotectedUsers[player.UserId] = nil
    if getgenv().lastHealths then
        getgenv().lastHealths[player.Name] = nil
    end
    if unbindSentryAssistPlayer then
        unbindSentryAssistPlayer(player)
    end
    return removed or true
end

local function collectSentryProtectedPlayers()
    local playersToCheck = {}
    local seenUserIds = {}

    local ownerPlayer = Players:FindFirstChild(Owner)
    if ownerPlayer then
        seenUserIds[ownerPlayer.UserId] = true
        table.insert(playersToCheck, ownerPlayer)
    end

    for userId, storedName in pairs(getgenv().sentryprotectedUsers) do
        local player = findPlayerByUserIdLocal(userId) or Players:FindFirstChild(storedName)
        if player then
            getgenv().sentryprotected[player.Name] = true
            getgenv().sentryprotectedUsers[player.UserId] = player.Name
            if not seenUserIds[player.UserId] then
                seenUserIds[player.UserId] = true
                table.insert(playersToCheck, player)
            end
        end
    end

    for storedName, enabled in pairs(getgenv().sentryprotected) do
        if enabled then
            local player = Players:FindFirstChild(storedName) or findPlayerByPartial(storedName)
            if player then
                getgenv().sentryprotectedUsers[player.UserId] = player.Name
                if not seenUserIds[player.UserId] then
                    seenUserIds[player.UserId] = true
                    table.insert(playersToCheck, player)
                end
            end
        end
    end

    return playersToCheck
end

local function refreshSentryProtectedBindings()
    if not bindSentryAssistPlayer then
        return
    end
    for _, protectedPlayer in ipairs(collectSentryProtectedPlayers()) do
        bindSentryAssistPlayer(protectedPlayer)
    end
end

Players.PlayerAdded:Connect(function(player)
    local storedName = getgenv().sentryprotectedUsers[player.UserId]
    local nameProtected = getgenv().sentryprotected[player.Name]
        or (storedName and tostring(storedName):lower() == player.Name:lower())
    if nameProtected and bindSentryAssistPlayer then
        getgenv().sentryprotected[player.Name] = true
        getgenv().sentryprotectedUsers[player.UserId] = player.Name
        bindSentryAssistPlayer(player)
    end
end)

Players.PlayerRemoving:Connect(function(player)
    if getgenv().lastHealths then
        getgenv().lastHealths[player.Name] = nil
    end
    if unbindSentryAssistPlayer then
        unbindSentryAssistPlayer(player.UserId)
    end
end)

local function compactShopToken(value)
    return tostring(value or ""):lower():gsub("[%s%[%]{}%-%$]", "")
end

local function findBrownBagTool()
    local lp = Players.LocalPlayer
    local backpack = lp and lp:FindFirstChild("Backpack")
    local char = lp and lp.Character

    local function scan(container)
        if not container then
            return nil
        end
        for _, child in ipairs(container:GetChildren()) do
            if child:IsA("Tool") then
                local lowerName = child.Name:lower()
                if lowerName:find("brownbag", 1, true) or lowerName:find("brown bag", 1, true) then
                    return child
                end
            end
        end
        return nil
    end

    return scan(char) or scan(backpack)
end

local function findBrownBagShopItem()
    local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
    if not shopFolder then
        return nil, nil, nil
    end

    local bestItem = nil
    local bestScore = -math.huge

    for _, child in ipairs(shopFolder:GetChildren()) do
        local lowerName = tostring(child.Name or ""):lower()
        if not lowerName:find("ammo", 1, true) then
            local compact = compactShopToken(lowerName)
            local score = nil
            if compact:find("brownbag", 1, true) then
                score = 100
            elseif lowerName:find("brown bag", 1, true) then
                score = 80
            end
            if score then
                if lowerName:find("28", 1, true) then
                    score = score + 20
                end
                if lowerName:find("[brownbag]", 1, true) or lowerName:find("{brownbag}", 1, true) then
                    score = score + 5
                end
                if score > bestScore then
                    bestScore = score
                    bestItem = child
                end
            end
        end
    end

    local clickDetector = bestItem and bestItem:FindFirstChildWhichIsA("ClickDetector", true)
    local shopBase = nil
    if clickDetector and clickDetector.Parent and clickDetector.Parent:IsA("BasePart") then
        shopBase = clickDetector.Parent
    elseif bestItem then
        local head = bestItem:FindFirstChild("Head")
        if head and head:IsA("BasePart") then
            shopBase = head
        else
            shopBase = bestItem:FindFirstChildWhichIsA("BasePart", true)
        end
    end
    return bestItem, clickDetector, shopBase
end

local function resolveBrownBagTarget(rawInput)
    local parsed = normalizePlayerInput(rawInput)
    if not parsed then
        return nil
    end
    local target = resolveDeliveryTargetPlayer(parsed) or findPlayerByPartial(parsed)
    if target == LocalPlayer then
        return nil
    end
    return target
end

local function buyBrownBagForCommand()
    local char = Player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (char and root and humanoid and humanoid.Health > 0) then
        return false
    end

    local bought = false
    withNoclip(function()
        root.AssemblyLinearVelocity = Vector3.zero
        root.AssemblyAngularVelocity = Vector3.zero
        root.CFrame = brownBagShopFallbackCFrame * CFrame.new(0, 2.8, 0)
        task.wait(0.04)

        for _ = 1, 10 do
            if findBrownBagTool() then
                bought = true
                break
            end

            local _, clickDetector, shopBase = findBrownBagShopItem()
            if clickDetector and shopBase then
                humanoid:UnequipTools()
                safeTeleportToShop(root, shopBase)
                getgenv().fireclickdetector(clickDetector)
            else
                root.AssemblyLinearVelocity = Vector3.zero
                root.AssemblyAngularVelocity = Vector3.zero
                root.CFrame = brownBagShopFallbackCFrame * CFrame.new(0, 2.8, 0)
            end
            task.wait(0.06)
        end
    end)

    return bought or (findBrownBagTool() ~= nil)
end

local function useBrownBagOnTarget(targetUserId)
    local activateCooldown = 0.05
    local lastActivateAt = 0
    local offsetIndex = 1
    local succeeded = false

    setNoclip(true)
    local ok, err = pcall(function()
        while brownBagActionInProgress and not hardStop do
            local bagTool = findBrownBagTool()
            if not bagTool then
                succeeded = true
                break
            end

            local char = Player.Character
            local root = char and char:FindFirstChild("HumanoidRootPart")
            local humanoid = char and char:FindFirstChildOfClass("Humanoid")
            if not (char and root and humanoid and humanoid.Health > 0) then
                task.wait(0.05)
                continue
            end

            local target = targetUserId and Players:GetPlayerByUserId(targetUserId) or nil
            local targetChar = target and target.Character
            local targetHum = targetChar and targetChar:FindFirstChildOfClass("Humanoid")
            local targetHRP = targetChar and targetChar:FindFirstChild("HumanoidRootPart")
            if not (target and targetChar and targetHum and targetHum.Health > 0 and targetHRP) then
                task.wait(0.06)
                continue
            end

            local offsetMode = offsetIndex
            offsetIndex = (offsetIndex % 4) + 1
            local offset
            if offsetMode == 1 then
                offset = (-targetHRP.CFrame.LookVector * 1.55) + Vector3.new(0, 1.55, 0)
            elseif offsetMode == 2 then
                offset = (targetHRP.CFrame.RightVector * 1.45) + Vector3.new(0, 1.5, 0)
            elseif offsetMode == 3 then
                offset = (-targetHRP.CFrame.RightVector * 1.45) + Vector3.new(0, 1.5, 0)
            else
                offset = (targetHRP.CFrame.LookVector * 1.2) + Vector3.new(0, 1.45, 0)
            end
            local standPos = targetHRP.Position + offset
            root.AssemblyLinearVelocity = Vector3.zero
            root.AssemblyAngularVelocity = Vector3.zero
            root.CFrame = CFrame.lookAt(standPos, targetHRP.Position + Vector3.new(0, 1.05, 0))

            if bagTool.Parent ~= char then
                bagTool.Parent = char
                pcall(function()
                    humanoid:EquipTool(bagTool)
                end)
                task.wait(0.02)
                bagTool = findBrownBagTool()
            end
            if not bagTool then
                succeeded = true
                break
            end

            local now = os.clock()
            if bagTool.Parent == char and (now - lastActivateAt) >= activateCooldown then
                pcall(function()
                    bagTool:Activate()
                end)
                lastActivateAt = now
            end

            task.wait(0.03)
        end
    end)
    setNoclip(false)
    if not ok then
        warn(err)
    end

    return succeeded or (findBrownBagTool() == nil)
end

handleBrownBagCommand = function(rawInput)
    if brownBagActionInProgress then
        sendMessage("BrownBag command is already running.")
        return
    end
    if buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress then
        sendMessage("BrownBag is busy. Try again in a moment.")
        return
    end

    local target = resolveBrownBagTarget(rawInput)
    if not target then
        sendMessage("Usage: .bag ;username;")
        return
    end

    brownBagActionInProgress = true
    brownBagTargetName = target.Name
    task.spawn(function()
        local prevEnabled = getgenv().enabled
        local prevTarget = targetPlayer
        local prevHome = standHomeName
        local prevVoiding = voiding
        local prevBuying = buyingInProgress
        local prevHardStop = hardStop

        local ok, err = pcall(function()
            hardStop = false
            cancelAttackModes()
            getgenv().enabled = false
            targetPlayer = nil
            voiding = false
            buyingInProgress = true

            if not findBrownBagTool() then
                sendMessage("Buying BrownBag for " .. target.Name .. "...")
                if not buyBrownBagForCommand() then
                    sendMessage("BrownBag buy failed.")
                    return
                end
            end

            local success = useBrownBagOnTarget(target.UserId)
            if success then
                sendMessage("BrownBag used on " .. target.Name .. ".")
            else
                sendMessage("BrownBag stopped before success on " .. target.Name .. ".")
            end
        end)

        buyingInProgress = prevBuying
        hardStop = prevHardStop
        brownBagActionInProgress = false
        brownBagTargetName = nil

        if prevEnabled then
            getgenv().enabled = true
            if prevHome then
                standHomeName = prevHome
                startFollowingTarget(prevHome)
            else
                targetPlayer = prevTarget
            end
            voiding = false
        else
            getgenv().enabled = false
            targetPlayer = prevTarget
            voiding = prevVoiding
        end

        if not ok then
            warn(err)
            sendMessage("BrownBag command error.")
        end
    end)
end

local function findFlamethrowerShopItem(wantAmmo)
    local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
    if not shopFolder then
        return nil, nil, nil
    end

    local preferredName = wantAmmo and FLAME_AMMO_ITEM_NAME or FLAME_SHOP_NAME
    local item = findShopItem(shopFolder, preferredName, {ammo = wantAmmo})

    if not item then
        for _, child in ipairs(shopFolder:GetChildren()) do
            local lowerName = tostring(child.Name or ""):lower()
            if lowerName:find("flamethrower", 1, true) then
                local isAmmo = lowerName:find("ammo", 1, true) ~= nil
                if isAmmo == wantAmmo then
                    item = child
                    break
                end
            end
        end
    end

    local clickDetector = item and item:FindFirstChildWhichIsA("ClickDetector", true)
    local shopBase = getShopBasePart(item, clickDetector)
    return item, clickDetector, shopBase
end

local function buyFlamethrowerForCommand()
    local char = Player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (char and root and humanoid and humanoid.Health > 0) then
        return false
    end

    if hasGun(FLAME_TOOL_NAME) then
        return true
    end

    local bought = false
    withNoclip(function()
        for _ = 1, 12 do
            if hasGun(FLAME_TOOL_NAME) then
                bought = true
                break
            end

            local _, clickDetector, shopBase = findFlamethrowerShopItem(false)
            humanoid:UnequipTools()
            if shopBase then
                safeTeleportToShop(root, shopBase)
            else
                safeTeleportToCFrame(root, flameShopFallbackCFrame)
            end
            if clickDetector then
                getgenv().fireclickdetector(clickDetector)
            end
            task.wait(0.14)
        end
    end)

    return bought or hasGun(FLAME_TOOL_NAME)
end

local function buyFlamethrowerAmmoForCommand(times)
    local char = Player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (char and root and humanoid and humanoid.Health > 0) then
        return
    end
    if not hasGun(FLAME_TOOL_NAME) then
        return
    end

    local buyCount = times or 6
    withNoclip(function()
        for _ = 1, buyCount do
            local _, clickDetector, shopBase = findFlamethrowerShopItem(true)
            humanoid:UnequipTools()
            if shopBase then
                safeTeleportToShop(root, shopBase)
            else
                safeTeleportToCFrame(root, flameAmmoFallbackCFrame)
            end
            if clickDetector then
                getgenv().fireclickdetector(clickDetector)
            end
            task.wait(0.1)
        end
    end)
end

local function prepareFlamethrowerLoadout()
    if type(purchaseArmor) == "function" and armorItems then
        purchaseArmor(armorItems.standard)
        purchaseArmor(armorItems.fire)
    end

    local prevBuying = buyingInProgress
    local prevGunBuying = buyingGunInProgress
    buyingInProgress = true
    buyingGunInProgress = true

    local ok, err = pcall(function()
        if not buyFlamethrowerForCommand() then
            return
        end

        buyFlamethrowerAmmoForCommand(6)
        equipTool(FLAME_TOOL_NAME)
        reloadTool()
    end)

    buyingGunInProgress = prevGunBuying
    buyingInProgress = prevBuying
    requestIdleVoidReturn(0.06)
    if not ok then
        warn(err)
        return false
    end
    return hasGun(FLAME_TOOL_NAME)
end

local function clearFlameModeState()
    flameModeActive = false
    flameModeTargetUserId = nil
    flameModeTargetName = nil
end

local function disableFlameMode(silent)
    if not flameModeActive and not (lockedTarget and flameModeTargetUserId and lockedTarget.UserId == flameModeTargetUserId) then
        if not silent then
            sendMessage("Flame mode is already off.")
        end
        return
    end

    clearFlameModeState()
    ragebottargets = {}
    shouldSwitch = false

    if not bringonly and not takeonly and not opkill and not flingonly and not getgenv().downonly and not stomponly then
        lockedTarget = nil
        lockedTargetUserId = nil
        teleporting = false
        if not resumeOwnerFollow() then
            voiding = true
        end
    end

    if not silent then
        sendMessage("Flame mode disabled.")
    end
end

local function activateFlameModeOnTarget(target)
    if not target then
        return false
    end
    if target == LocalPlayer then
        sendMessage("Cannot flame yourself.")
        return false
    end
    if isProtected(target) then
        sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
        return false
    end

    hardStop = false
    cancelAttackModes()

    commandSender = Owner
    flameModeActive = true
    flameModeTargetUserId = target.UserId
    flameModeTargetName = target.Name

    lockedTarget = target
    lockedTargetUserId = target.UserId
    teleporting = true
    voiding = false
    summonTarget = nil
    stomponly = false
    bringonly = false
    takeonly = false
    getgenv().downonly = false
    opkill = false
    flingonly = false
    killall = false
    ragebottargets = {}
    shouldSwitch = false
    skyTarget = nil
    savedTarget5 = nil
    forceBringDrop = false

    task.spawn(function()
        local success = prepareFlamethrowerLoadout()
        if not flameModeActive then
            return
        end
        local currentTarget = Players:GetPlayerByUserId(flameModeTargetUserId or 0) or target
        if currentTarget and currentTarget ~= lockedTarget then
            lockedTarget = currentTarget
            lockedTargetUserId = currentTarget.UserId
        end
        if not success then
            sendMessage("Flame loadout failed. Check gun/ammo shop visibility.")
        else
            sendMessage("Flame mode locked on " .. (currentTarget and currentTarget.Name or target.Name) .. ".")
        end
    end)

    return true
end

local function resolveSmiteTarget(rawInput)
    local parsed = normalizePlayerInput(rawInput)
    if not parsed then
        return nil, nil
    end
    parsed = parsed:gsub("^[:;]+", ""):gsub("[:;]+$", "")
    parsed = trimInput(parsed)
    if not parsed or parsed == "" then
        return nil, nil
    end
    local target = resolveDeliveryTargetPlayer(parsed) or findPlayerByPartial(parsed)
    if target == LocalPlayer or (target and target.Name == Owner) then
        return nil, parsed
    end
    return target, parsed
end

local function isSmiteTargetOutOfMap(target)
    if not target then
        return true
    end
    local targetChar = target.Character
    if not targetChar then
        return false
    end
    local targetHRP = targetChar:FindFirstChild("HumanoidRootPart")
    if targetHRP then
        local pos = targetHRP.Position
        if pos.Y <= SMITE_OUT_OF_MAP_MIN_Y or pos.Y >= SMITE_OUT_OF_MAP_MAX_Y then
            return true
        end
        if math.abs(pos.X) >= SMITE_OUT_OF_MAP_XZ or math.abs(pos.Z) >= SMITE_OUT_OF_MAP_XZ then
            return true
        end
    end
    local bodyEffects = targetChar:FindFirstChild("BodyEffects")
    local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
    return isSDeath or false
end

handleSmiteCommand = function(rawInput)
    if buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress then
        sendMessage("Smite is busy. Try again in a moment.")
        return
    end

    local target, parsedInput = resolveSmiteTarget(rawInput)
    if not parsedInput then
        sendMessage("Usage: .smite :username:")
        return
    end
    if not target then
        sendMessage("Could not find " .. parsedInput)
        return
    end
    if isProtected(target) then
        sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
        return
    end

    local previousEnabled = getgenv().enabled
    local previousHome = standHomeName
    local previousTarget = targetPlayer

    hardStop = false
    cancelAttackModes()

    smiteRunId += 1
    local runId = smiteRunId
    smiteCommandInProgress = true
    smiteTargetUserId = target.UserId
    smiteTargetName = target.Name

    getgenv().enabled = false
    targetPlayer = nil
    lockedTarget = target
    teleporting = true
    voiding = false
    flingonly = true

    local currentChar = LocalPlayer.Character
    local currentHumanoid = currentChar and currentChar:FindFirstChildOfClass("Humanoid")
    if currentHumanoid then
        currentHumanoid:UnequipTools()
    end

    sendMessage("Smite locked on " .. target.Name)
    setStandGhost(true)
    setNoclip(true)
    markCombatLoadoutDemand(4.2)
    requestImmediateCombatLoadoutPrime()

    task.spawn(function()
        local success = false
        local overridden = false
        local finalTargetName = target.Name
        local function endSmiteMobility()
            if not smiteCommandInProgress then
                setNoclip(false)
                setStandGhost(false)
            end
        end

        for attempt = 1, SMITE_MAX_ATTEMPTS do
            local stopAt = os.clock() + SMITE_ATTEMPT_DURATION
            while os.clock() < stopAt do
                if smiteRunId ~= runId or not smiteCommandInProgress then
                    endSmiteMobility()
                    return
                end

                if not flingonly then
                    overridden = true
                    break
                end

                local activeTarget = smiteTargetUserId and Players:GetPlayerByUserId(smiteTargetUserId) or nil
                if not activeTarget then
                    success = true
                    break
                end
                finalTargetName = activeTarget.Name

                if lockedTarget and lockedTarget.UserId ~= smiteTargetUserId then
                    overridden = true
                    break
                end
                if not lockedTarget or lockedTarget.UserId ~= smiteTargetUserId then
                    lockedTarget = activeTarget
                end

                local myChar = LocalPlayer.Character
                local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
                local myHumanoid = myChar and myChar:FindFirstChildOfClass("Humanoid")
                local targetChar = activeTarget.Character
                local targetHRP = targetChar and targetChar:FindFirstChild("HumanoidRootPart")

                if myHumanoid then
                    myHumanoid:UnequipTools()
                end

                if myHRP and targetHRP then
                    local targetVelocity = targetHRP.AssemblyLinearVelocity or targetHRP.Velocity or Vector3.zero
                    local predictedPos = targetHRP.Position + (targetVelocity * SMITE_PREDICT_TIME)
                    local touchOffset = Vector3.new(
                        (math.random(-100, 100) / 100) * SMITE_TOUCH_RADIUS,
                        math.random(-40, 40) / 100,
                        (math.random(-100, 100) / 100) * SMITE_TOUCH_RADIUS
                    )
                    local chasePos = predictedPos + touchOffset
                    myHRP.AssemblyLinearVelocity = Vector3.zero
                    myHRP.AssemblyAngularVelocity = Vector3.zero
                    moveStandToCFrameExact(myChar, myHRP, CFrame.new(chasePos))
                    resetPartVelocity(myHRP)
                end

                if isSmiteTargetOutOfMap(activeTarget) then
                    success = true
                    break
                end

                task.wait(SMITE_TRACK_INTERVAL)
            end

            if success or overridden then
                break
            end
            if attempt < SMITE_MAX_ATTEMPTS then
                task.wait(0.2)
            end
        end

        if smiteRunId ~= runId then
            endSmiteMobility()
            return
        end

        cancelSmiteCommandState()
        endSmiteMobility()

        if overridden then
            return
        end

        if lockedTarget and lockedTarget.UserId == target.UserId then
            lockedTarget = nil
        end
        flingonly = false
        teleporting = false
        voiding = true

        if previousEnabled then
            getgenv().enabled = true
            standHomeName = previousHome or Owner
            targetPlayer = previousTarget
            startFollowingTarget(standHomeName)
            voiding = false
        else
            getgenv().enabled = false
            targetPlayer = previousTarget
        end

        if success then
            sendMessage("Smite finished on " .. finalTargetName .. ".")
        else
            sendMessage("Smite ended. Target not forced out after 2 tries.")
        end
    end)
end

function setupChatListener(player)
    if not isAuthorized(player) then return end

    if not playerChatConnections[player.UserId] then
        playerChatConnections[player.UserId] = player.Chatted:Connect(function(message)
            if not isAuthorized(player) then
                return
            end
            dispatchAuthorizedChatMessage({
                Text = tostring(message or ""),
                TextSource = {
                    UserId = player.UserId,
                },
            }, "chatted")
        end)
    end

    activeListeners[player.UserId] = function(msg)
        local sender = msg.TextSource and msg.TextSource.UserId and Players:GetPlayerByUserId(msg.TextSource.UserId)
        if not sender or sender ~= player then return end

        local message = msg.Text or ""
        local msgLower = message:lower()

        local passiveOwnerControlCommand = msgLower == ".a off"
            or msgLower == ".sentry on"
            or msgLower == ".sentry off"
            or msgLower == ".bsentry on"
            or msgLower == ".bsentry off"
            or msgLower == ".leave"
            or msgLower == ".v"
            or msgLower:match("^%.v%s+")
            or msgLower == ".abuse on"
            or msgLower == ".abuse off"
            or msgLower == ".fp on"
            or msgLower == ".fp off"
            or msgLower == ".autosave on"
            or msgLower == ".autosave off"
            or msgLower:match("^%.assist%s+")
            or msgLower:match("^%.unassist%s+")
            or msgLower:match("^%.wl%s+")
            or msgLower:match("^%.unwl%s+")
            or msgLower:match("^%.awl%s+")
            or msgLower:match("^%.unawl%s+")
            or msgLower:match("^%.akill%s+off%s*$")
            or msgLower == ".stand off"

        if (isAuthorized(player)) then
            if msgLower:sub(1, 1) == "." and not passiveOwnerControlCommand then
                clearManualVoidHold()
                markStandCommandBusy(4.5)
            end
            if msgLower == ".a on" then
                clearPendingOwnerFollowResume()
                clearPendingKOTaskResume()
                postResetCombatRecoveryActive = false
                postResetCombatRecoveryUntil = 0
                postResetLoadoutGraceUntil = 0
                hardStop = false
                cancelAttackModes()
                lockedTarget = nil
                lockedTargetUserId = nil
                summonTarget = nil
                teleporting = false
                voiding = false
                getgenv().enabled = true
                targetPlayer = player
                standHomeName = player.Name
                followShotsPerTick = math.max(followShotsPerTick or 1, ownerFollowShotsPerTick or 2)
                followShotCooldown = math.min(followShotCooldown or 0.08, ownerFollowShotCooldown or 0.04)
                followGunSpacing = math.min(followGunSpacing or 0.01, ownerFollowGunSpacing or 0.006)
                reloadCooldown = math.min(reloadCooldown or 0.4, ownerFollowReloadCooldown or 0.24)
                startFollowingTarget(player.Name)
                resetRespawnFireState()
                resetCombatFireWindow()
                local currentCharacter = Player and Player.Character
                local currentBackpack = Player and Player:FindFirstChild("Backpack")
                if currentCharacter then
                    equipRespawnCombatLoadout(currentCharacter, currentBackpack)
                end
                equipConfiguredGuns()
                reloadTool()
                if currentCharacter and hasUsableCombatLoadout(currentCharacter, currentBackpack) then
                    postResetCombatRecoveryActive = false
                    postResetCombatRecoveryUntil = 0
                else
                    postResetCombatRecoveryActive = true
                    postResetCombatRecoveryUntil = math.max(postResetCombatRecoveryUntil or 0, os.clock() + 4)
                end
                requestImmediateCombatLoadoutPrime()
                requestOwnerFollowLoadoutPrimeBurst()
                if primeCombatLoadoutAfterRespawn and currentCharacter then
                    task.delay(0.08, function()
                        if getgenv().enabled and Player and Player.Character == currentCharacter and not hardStop then
                            primeCombatLoadoutAfterRespawn(currentCharacter)
                        end
                    end)
                end
                if stand2Active and standHomeName ~= player.Name then
                    standHomeName = player.Name
                end
            elseif msgLower == ".a off" then
                clearPendingOwnerFollowResume()
                clearPendingKOTaskResume()
                postResetCombatRecoveryActive = false
                postResetCombatRecoveryUntil = 0
                cancelAttackModes()
                getgenv().enabled = false
                -- send stand back to void
                voiding = true
                teleporting = false
                lockedTarget = nil
                summonTarget = nil
                if disableStand2 then
                    disableStand2()
                end
            elseif msgLower:match("^%.stand2") then
                local rawInput = message:match("^%.stand2%s*;?%s*([^;]+)") or message:match("^%.stand2%s+(.+)$")
                rawInput = trimInput(rawInput)
                if rawInput and handleStand2Command then
                    handleStand2Command(rawInput)
                else
                    sendMessage("stand2 needs a target name.")
                end
            elseif msgLower == ".stand off" then
                if disableStand2 then
                    disableStand2()
                end
            elseif msgLower == ".sentry on" then
                hardStop = false
                cancelAttackModes()
                lockedTarget = nil
                voiding = false
                getgenv().enabled1 = true
                refreshSentryProtectedBindings()
                markCombatLoadoutDemand(3.2)
                requestImmediateCombatLoadoutPrime()
                sendMessage("Sentry enabled.")
            elseif msgLower == ".sentry off" then
                cancelAttackModes()
                getgenv().enabled1 = false
                sentrytarget = nil
                voiding = true
                sendMessage("Sentry disabled.")
            elseif msgLower == ".bsentry on" then      
                if not getgenv().enabled1 then
                    sendMessage("Turn .sentry on first.")
                    return
                end
                for plrName, _ in pairs(Bots) do
                    local botPlayer = Players:FindFirstChild(plrName)
                    if botPlayer then
                        rememberSentryProtectedPlayer(botPlayer)
                    else
                        getgenv().sentryprotected[plrName] = true
                    end
                end
                refreshSentryProtectedBindings()
                sendMessage("Bot sentry enabled.")
            elseif msgLower == ".bsentry off" then      
                for plrName, _ in pairs(Bots) do
                    local botPlayer = Players:FindFirstChild(plrName)
                    if botPlayer then
                        forgetSentryProtectedPlayer(botPlayer)
                    else
                        getgenv().sentryprotected[plrName] = nil
                        if getgenv().lastHealths then
                            getgenv().lastHealths[plrName] = nil
                        end
                    end
                end
                sendMessage("Bot sentry disabled.")
            elseif msgLower == ".reset" then
                handleResetCommand()
            elseif msgLower:match("^%.reset%s+([^%s]+)$") then
                local botName = msgLower:match("^%.reset%s+([^%s]+)$")
                handleResetCommand(botName)
            elseif msgLower == ".repair" then
                handleFixCommand()
            elseif msgLower:match("^%.repair%s+([^%s]+)$") then
                local botName = msgLower:match("^%.repair%s+([^%s]+)$")
                handleFixCommand(botName)
            elseif msgLower == ".v" then
                handleHideCommand()
            elseif msgLower:match("^%.v%s+([^%s]+)$") then
                local botName = msgLower:match("^%.v%s+([^%s]+)$")
                handleHideCommand(botName)
            elseif msgLower == ".summon" then
                handleTeleportCommand(player.Name)
            elseif msgLower:match("^%.summon%s+([^%s]+)$") then
                local botName = msgLower:match("^%.summon%s+([^%s]+)$")
                handleTeleportCommand(player.Name, botName)
            elseif msgLower:match("^%.to%s+(.+)$") or msgLower:match("^%.tp%s+(.+)$") then
                if player.Name ~= Owner then return end
                clearManualVoidHold()
                hardStop = false
                invalidateToDeliveryRun()
                local destination = msgLower:match("^%.to%s+(.+)$") or msgLower:match("^%.tp%s+(.+)$")
                destination = trimInput(destination)
                if destination and destination ~= "" then
                    local resolvedCFrame = locationCFrames[destination:lower()]
                    local resolvedTargetPlayer = nil
                    local resolvedTargetHRP = nil
                    if not resolvedCFrame then
                        resolvedTargetPlayer = resolveDeliveryTargetPlayer(destination)
                        resolvedTargetHRP = getPlayerDestinationPart(resolvedTargetPlayer)
                        if not resolvedTargetHRP then
                            sendMessage("Delivery target not found. Use exact/unique player name or a saved location.")
                            return
                        end
                    end

                    local hadActiveDelivery = toDeliveryActive
                    if hadActiveDelivery then
                        clearDeliveryResumeState()
                    else
                        captureDeliveryResumeState()
                    end
                    resetBringGrabAttemptState()
                    pcall(function()
                        ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                    end)
                    lockedTarget = nil
                    lockedTargetUserId = nil
                    bringonly = false
                    takeonly = false
                    teleporting = false
                    forceBringDrop = false
                    toDeliveryActive = false
                    lastToDestination = nil
                    lastToDropCFrame = nil
                    vehicleMode = false
                    gotoPlayer = nil
                    gotoTarget = nil
                    gotoTargetUserId = nil
                    gotoCFrame = nil
                    vehicleModel = nil
                    task.wait(0.05)
                    forceBringDrop = false
                    toDeliveryActive = true
                    lastToDestination = destination
                    lastToDropCFrame = nil
                    -- Kill owner first with retry logic
                    local ownerPlr = Players:FindFirstChild(Owner)
                    if not ownerPlr then
                        toDeliveryActive = false
                        lastToDestination = nil
                        lastToDropCFrame = nil
                        forceBringDrop = false
                        resetBringGrabAttemptState()
                        restoreDeliveryResumeState()
                        return
                    end
                    local ownerKO = false
                    if ownerPlr and ownerPlr.Character then
                        local bodyEffects = ownerPlr.Character:FindFirstChild("BodyEffects")
                        local koValue = bodyEffects and bodyEffects:FindFirstChild("K.O")
                        ownerKO = koValue and koValue.Value or false
                        if isHoldingTarget(ownerPlr.Character) then
                            forceBringDrop = true
                        end
                    end
                    if ownerPlr and ownerPlr.Character then
                        local ownerHum = ownerPlr.Character:FindFirstChildOfClass("Humanoid")
                        if ownerHum and not ownerKO then
                            -- Multiple kill attempts to ensure it works
                            for killAttempt = 1, 5 do
                                if ownerHum.Health > 0 then
                                    ownerHum.Health = 0
                                    task.wait(0.12)
                                else
                                    break
                                end
                            end

                            local koDeadline = os.clock() + 0.55
                            repeat
                                local liveBodyEffects = ownerPlr.Character and ownerPlr.Character:FindFirstChild("BodyEffects")
                                local liveKOValue = liveBodyEffects and liveBodyEffects:FindFirstChild("K.O")
                                ownerKO = (liveKOValue and liveKOValue.Value) or ownerHum.Health <= 0
                                if ownerKO then
                                    break
                                end
                                task.wait(0.03)
                            until os.clock() >= koDeadline
                        end
                    end
                    -- Then grab and bring owner to destination
                    commandSender = Owner
                    lockedTarget = ownerPlr
                    lockedTargetUserId = ownerPlr.UserId
                    resetBringGrabAttemptState()
                    requestPostCarryCombatRecovery(lockedTarget or sentrytarget, true)
                    reloadTool()
                    stomponly = false
                    bringonly = true
                    takeonly = false
                    getgenv().downonly = false
                    opkill = false
                    voiding = false
                    summonTarget = nil
                    flingonly = false
                    killall = false
                    ragebottargets = {}
                    shouldSwitch = false
                    teleporting = true
                    flameModeActive = false
                    flameModeTargetUserId = nil
                    flameModeTargetName = nil
                    skyTarget = nil
                    savedTarget5 = nil
                    if ownerKO then
                        forceBringDrop = true
                    end
                    -- Set destination for bring logic
                    gotoCFrame = resolvedCFrame
                    gotoTarget = nil
                    gotoTargetUserId = nil
                    if gotoCFrame then
                        lastToDropCFrame = gotoCFrame
                    else
                        gotoTarget = resolvedTargetPlayer
                        gotoTargetUserId = resolvedTargetPlayer and resolvedTargetPlayer.UserId or nil
                        if resolvedTargetHRP then
                            lastToDropCFrame = CFrame.new(resolvedTargetHRP.Position)
                        end
                    end
                end
            elseif msgLower:match("^%.bag") then
                if player.Name ~= Owner then return end
                local rawBagTarget = message:match("^%.bag%s*;%s*([^;]+)%s*;?%s*$") or message:match("^%.bag%s+(.+)$")
                rawBagTarget = normalizePlayerInput(rawBagTarget)
                if not rawBagTarget then
                    sendMessage("Usage: .bag ;username;")
                    return
                end
                handleBrownBagCommand(rawBagTarget)
            elseif msgLower:match("^%.smite%s+off%s*$") then
                if player.Name ~= Owner then return end
                local previousSmiteTargetUserId = smiteTargetUserId
                cancelSmiteCommandState()
                if flingonly then
                    flingonly = false
                end
                if lockedTarget and previousSmiteTargetUserId and lockedTarget.UserId == previousSmiteTargetUserId then
                    lockedTarget = nil
                end
                teleporting = false
                voiding = true
                sendMessage("Smite off.")
            elseif msgLower:match("^%.smite") then
                if player.Name ~= Owner then return end
                local rawSmiteTarget = message:match("^%.smite%s*[:;]%s*([^:;]+)%s*[:;]?%s*$")
                    or message:match("^%.smite%s+(.+)$")
                rawSmiteTarget = normalizePlayerInput(rawSmiteTarget)
                if not rawSmiteTarget then
                    sendMessage("Usage: .smite :username:")
                    return
                end
                handleSmiteCommand(rawSmiteTarget)
            elseif msgLower:match("^%.f%s+off%s*$") then
                if player.Name ~= Owner then return end
                disableFlameMode()
            elseif msgLower:match("^%.f%s*$") then
                if player.Name ~= Owner then return end
                sendMessage("Usage: .f ;username;")
            elseif msgLower:match("^%.f%s*;") or msgLower:match("^%.f%s+.+$") then
                if player.Name ~= Owner then return end
                local rawFlameTarget = message:match("^%.f%s*;%s*([^;]+)%s*;?%s*$")
                    or message:match("^%.f%s+(.+)$")
                rawFlameTarget = normalizePlayerInput(rawFlameTarget)
                if not rawFlameTarget then
                    sendMessage("Usage: .f ;username;")
                    return
                end
                local target = resolveDeliveryTargetPlayer(rawFlameTarget) or findPlayerByPartial(rawFlameTarget)
                if not target then
                    sendMessage("Could not find " .. rawFlameTarget)
                    return
                end
                activateFlameModeOnTarget(target)
            elseif msgLower == ".s" then
                teleportToTarget(player.Name)
            elseif msgLower == ".search" then
                lockedTarget = nil
                voiding = false
                teleportPlayerRandomly()
                task.wait(1)
                checkWhitelistNearPosition()
                task.wait(1)
                voiding = true
            elseif msgLower == ".cashdrop on" then
                autodrop = true
            elseif msgLower == ".cashdrop off" then
                autodrop = false
            elseif msgLower == ".abuse on" then
                AbuseProtection = true
                abuseProtectionCooldownUntil = os.clock() + 0.5
                sendMessage("Abuse protection enabled.")
            elseif msgLower == ".abuse off" then
                AbuseProtection = false
                abuseProtectionCooldownUntil = 0
                sendMessage("Abuse protection disabled.")
            elseif msgLower == ".mask on" then
                automaskenabled = true
            elseif msgLower == ".mask off" then
                automaskenabled = false
            elseif EMOTES[msgLower] then
                playAnimation(EMOTES[msgLower])
            elseif msgLower == ".stop" then
                if currentTrack then
                    currentTrack:Stop()
                    currentTrack = nil
                end
                lastEmote = nil
            elseif msgLower == ".fp on" then
                setfflag("NextGenReplicatorEnabledWrite4", "true")
                task.wait(0.1)
                replicatesignal(game.Players.LocalPlayer.Kill)
            elseif msgLower == ".fp off" then
                setfflag("NextGenReplicatorEnabledWrite4", "false")
                task.wait(0.1)
                replicatesignal(game.Players.LocalPlayer.Kill)
            elseif msgLower == ".stand perf on" or msgLower == ".perf on" or msgLower == ".sp on" then
                if activateStandPerformanceMode then
                    activateStandPerformanceMode(true)
                end
            elseif msgLower == ".stand perf off" or msgLower == ".perf off" or msgLower == ".sp off" then
                if deactivateStandPerformanceMode then
                    deactivateStandPerformanceMode()
                end
            elseif msgLower == ".stand perf" or msgLower == ".perf" or msgLower == ".sp" then
                if standPerformanceModeActive then
                    if deactivateStandPerformanceMode then
                        deactivateStandPerformanceMode()
                    end
                elseif activateStandPerformanceMode then
                    activateStandPerformanceMode()
                end
            elseif msgLower == "power!" or msgLower == ".power!" then
                -- Only allow POWER MODE toggling when stand follow is OFF
                if getgenv().enabled then
                    sendMessage("Turn .a off to use POWER MODE.")
                else
                    if activatePowerMode then
                        activatePowerMode()
                    end
                end
            elseif msgLower == ".autosave on" or msgLower == "autosave!" then
                autoSaveEnabled = true
                sendMessage("Autosave enabled - will save owner when knocked")
            elseif msgLower == ".autosave off" then
                autoSaveEnabled = false
                sendMessage("Autosave disabled")
            elseif msgLower == ".leave" then
                game:Shutdown()
            elseif msgLower == ".rejoin" then
                TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, LocalPlayer)
            elseif msgLower:match("^%.say%s+(.+)$") then
                local messageToSay = msgLower:match("^%.say%s+(.+)$")
                sendMessage(messageToSay)
            elseif msgLower:match("^%.awl%s+([^%s]+)$") then
                local input = msgLower:match("^%.awl%s+([^%s]+)$")
                local target = findPlayerByPartial(input)
                if target then
                    getgenv().whitelist[target.Name] = true
                    sendMessage("Whitelisted " .. target.Name)
                else
                    sendMessage("Could not find " .. input .. " to whitelist")
                end
            elseif msgLower:match("^%.unawl%s+([^%s]+)$") then
                local input = msgLower:match("^%.unawl%s+([^%s]+)$")
                local target = findPlayerByPartial(input)
                if target then
                    getgenv().whitelist[target.Name] = nil
                    sendMessage("Unwhitelisted " .. target.Name)
                else
                    sendMessage("Could not find " .. input .. " to unwhitelist")
                end
            elseif msgLower:match("^%.assist%s+(.+)$") then
                local raw = message:match("^%.assist%s+(.+)$")
                raw = normalizePlayerInput(raw)
                if not raw then
                    sendMessage("Usage: .assist username")
                    return
                end
                local target = findPlayerByExactOrPartial(raw)
                if not target then
                    sendMessage("Could not find " .. raw)
                    return
                end
                rememberSentryProtectedPlayer(target)
                if getgenv().enabled1 then
                    sendMessage("Assist enabled for " .. target.Name)
                else
                    sendMessage("Assist enabled for " .. target.Name .. " (turn .sentry on to activate)")
                end
            elseif msgLower:match("^%.unassist%s+(.+)$") then
                local raw = message:match("^%.unassist%s+(.+)$")
                raw = normalizePlayerInput(raw)
                if not raw then
                    sendMessage("Usage: .unassist username")
                    return
                end
                local target = findPlayerByExactOrPartial(raw)
                if target then
                    forgetSentryProtectedPlayer(target)
                    sendMessage("Assist disabled for " .. target.Name)
                elseif forgetSentryProtectedName(raw) then
                    sendMessage("Assist disabled for " .. raw)
                else
                    sendMessage("Could not find " .. raw)
                end
            elseif msgLower:match("^%.l%s+([^%s]+)$") then
                hardStop = false
                -- Loopkill: single target (.l username) - uses improved fly system with stomp
                local inputName = msgLower:match("^%.l%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end

                -- Reset state and set single target
                reloadTool()
                lockedTarget = target

                -- .l uses improved fly system with stomp after knock
                stomponly = true
                bringonly = false
                takeonly = false
                getgenv().downonly = false
                opkill = false
                flingonly = false
                killall = false
                voiding = false
                summonTarget = nil

                ragebottargets = {target}
                shouldSwitch = false
                followState.currentTargetId = target.UserId
                resetFollowPrediction()
                lastShootAt = 0
                markCombatLoadoutDemand(3.6)
                requestCombatAttackPrime(target, true)

                teleporting = true
                voiding = false

            -- POWER-MODE SAFE DIRECT COMBAT COMMANDS (no bot checks)
            elseif msgLower:match("^%.d%s+([^%s]+)$") then
                hardStop = false
                local inputName = msgLower:match("^%.d%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end
                reloadTool()
                lockedTarget = target
                teleporting = true
                voiding = false
                summonTarget = nil
                ragebottargets = {}
                shouldSwitch = false
                followState.currentTargetId = target.UserId
                resetFollowPrediction()
                lastShootAt = 0
                markCombatLoadoutDemand(3.6)
                requestCombatAttackPrime(target, true)
                stomponly = false
                bringonly = false
                takeonly = false
                opkill = false
                flingonly = false
                killall = false
                getgenv().downonly = true

            elseif msgLower:match("^%.b%s*$") then
                sendMessage("Usage: .b ;username;")
            elseif msgLower:match("^%.b%s*;") or msgLower:match("^%.b%s+.+$") then
                hardStop = false
                cancelSmiteCommandState()
                local rawBringTarget = message:match("^%.b%s*;%s*([^;]+)%s*;?%s*$")
                    or message:match("^%.b%s+(.+)$")
                local target, parsedBringTarget = resolveBringCommandTarget(rawBringTarget)
                if not target then
                    if parsedBringTarget then
                        sendMessage("Could not find " .. parsedBringTarget)
                    else
                        sendMessage("Usage: .b ;username;")
                    end
                    return
                end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end
                resetBringGrabAttemptState()
                pcall(function()
                    ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                end)
                commandSender = Owner
                local ownerDestination = Players:FindFirstChild(Owner)
                -- Ensure the target is knocked but do not start teleporting to the drop location until after grab.
                tryForceBringKO(target, 0)
                reloadTool()
                lockedTarget = target
                lockedTargetUserId = target.UserId
                -- For bring commands we should not immediately teleport to the owner.
                -- Set teleporting to false so the stand approaches the target normally.
                teleporting = false
                voiding = false
                summonTarget = nil
                ragebottargets = {}
                shouldSwitch = false
                vehicleMode = false
                gotoPlayer = nil
                vehicleModel = nil
                clearDeliveryResumeState()
                stomponly = false
                bringonly = true
                takeonly = false
                opkill = false
                flingonly = false
                killall = false
                getgenv().downonly = false
                flameModeActive = false
                flameModeTargetUserId = nil
                flameModeTargetName = nil
                skyTarget = nil
                savedTarget5 = nil
                toDeliveryActive = false
                lastToDestination = nil
                lastToDropCFrame = nil
                forceBringDrop = false
                -- Do not set gotoTarget until the target is successfully grabbed.
                gotoCFrame = nil
                gotoTarget = nil
                gotoTargetUserId = nil
                -- Store the intended destination so we can apply it after grabbing.
                pendingGotoTarget = ownerDestination
                pendingGotoTargetUserId = ownerDestination and ownerDestination.UserId or nil

            elseif msgLower:match("^%.s%s+([^%s]+)$") then
                hardStop = false
                local inputName = msgLower:match("^%.s%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end
                reloadTool()
                lockedTarget = target
                teleporting = true
                voiding = false
                summonTarget = nil
                ragebottargets = {}
                shouldSwitch = false
                followState.currentTargetId = target.UserId
                resetFollowPrediction()
                lastShootAt = 0
                markCombatLoadoutDemand(3.6)
                requestCombatAttackPrime(target, true)
                stomponly = true
                bringonly = false
                takeonly = false
                opkill = false
                flingonly = false
                killall = false
                getgenv().downonly = false

            elseif msgLower:match("^%.sky%s+([^%s]+)$") then
                hardStop = false
                local inputName = msgLower:match("^%.sky%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end
                skyTarget = target
                reloadTool()
                lockedTarget = target
                teleporting = true
                voiding = false
                summonTarget = nil
                ragebottargets = {}
                shouldSwitch = false
                followState.currentTargetId = target.UserId
                resetFollowPrediction()
                lastShootAt = 0
                markCombatLoadoutDemand(3.6)
                requestCombatAttackPrime(target, true)
                stomponly = false
                bringonly = false
                takeonly = true
                opkill = false
                flingonly = false
                killall = false
                getgenv().downonly = false
            elseif msgLower:match("^%.lk%s+([^%s]+)$") then
                hardStop = false
                -- Loopknock: single-argument form (.lk username)
                local inputName = msgLower:match("^%.lk%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end

                reloadTool()
                lockedTarget = target
                teleporting = true
                voiding = false
                summonTarget = nil

                -- modes
                stomponly = false
                bringonly = false
                takeonly = false
                getgenv().downonly = true
                opkill = false
                flingonly = false
                killall = false

                ragebottargets = {target}
                shouldSwitch = false
                followState.currentTargetId = target.UserId
                resetFollowPrediction()
                lastShootAt = 0
                markCombatLoadoutDemand(3.6)
                requestCombatAttackPrime(target, true)

            elseif msgLower:match("^%.lk%s+([^%s]+)%s+([^%s]+)$") then
                hardStop = false
                -- Loopknock: legacy two-argument form (.lk username botName)
                local inputName = msgLower:match("^%.lk%s+([^%s]+)%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end

                reloadTool()
                lockedTarget = target
                teleporting = true
                voiding = false
                summonTarget = nil

                -- modes
                stomponly = false
                bringonly = false
                takeonly = false
                getgenv().downonly = true
                opkill = false
                flingonly = false
                killall = false

                ragebottargets = {target}
                shouldSwitch = false
                followState.currentTargetId = target.UserId
                resetFollowPrediction()
                lastShootAt = 0
                markCombatLoadoutDemand(3.6)
                requestCombatAttackPrime(target, true)
            elseif msgLower:match("^%.right%s+([^%s]+)$") then
                local targetName = msgLower:match("^%.right%s+([^%s]+)$")
                
                local myName = LocalPlayer.Name:lower()
                local myDisplay = LocalPlayer.DisplayName:lower()

                if myName:find(targetName, 1, true) or myDisplay:find(targetName, 1, true) then
                    summonMode = "right"
                end

            elseif msgLower:match("^%.left%s+([^%s]+)$") then
                local targetName = msgLower:match("^%.left%s+([^%s]+)$")
                
                local myName = LocalPlayer.Name:lower()
                local myDisplay = LocalPlayer.DisplayName:lower()

                if myName:find(targetName, 1, true) or myDisplay:find(targetName, 1, true) then
                    summonMode = "left"
                end

            elseif msgLower:match("^%.middle%s+([^%s]+)$") then
                local targetName = msgLower:match("^%.middle%s+([^%s]+)$")
                
                local myName = LocalPlayer.Name:lower()
                local myDisplay = LocalPlayer.DisplayName:lower()

                if myName:find(targetName, 1, true) or myDisplay:find(targetName, 1, true) then
                    summonMode = "middle"
                end
            elseif msgLower:match("^%.fling%s+([^%s]+)$") then
                hardStop = false
                local inputName = msgLower:match("^%.fling%s+([^%s]+)$")
                local target = findPlayerByPartial(inputName)
                if not target then return end
                if isProtected(target) then
                    sendMessage("Cannot target user " .. target.Name .. " because they are premium.")
                    return
                end
                reloadTool()
                lockedTarget = target
                teleporting = true
                voiding = false
                summonTarget = nil
                stomponly = false
                bringonly = false
                takeonly = false
                getgenv().downonly = false
                opkill = false
                flingonly = true
                killall = false
            elseif msgLower:match("^%.akill%s+on$") then
                hardStop = false
                -- Kill all: enable killall loop and ensure we are not in another mode
                killall = true
                summonTarget = nil
                teleporting = true
                voiding = false
                stomponly = false
                bringonly = false
                takeonly = false
                getgenv().downonly = false
                opkill = false
                flingonly = false
            elseif msgLower:match("^%.akill%s+off$") then
                killall = false
                lockedTarget = nil
                teleporting = false
                voiding = true
            -- Removed duplicate legacy combat handlers below.
            -- The primary handlers earlier in this chain are the ones used.
            elseif msgLower:match("^%.wl%s+(.+)$") then
                if player.Name ~= Owner then return end
                local raw = message:match("^%.wl%s+(.+)$")
                raw = normalizePlayerInput(raw)
                if not raw then
                    sendMessage("Usage: .wl \"username\"")
                    return
                end
                local target = findPlayerByPartial(raw)
                if not target then
                    sendMessage("Could not find " .. raw .. " to whitelist")
                    return
                end
                whitelistedUsers[target.Name] = true
                setupChatListener(target)
                sendMessage("Allowed " .. target.Name .. " to use your stand")
            elseif msgLower:match("^%.unwl%s+(.+)$") then
                if player.Name ~= Owner then return end
                local raw = message:match("^%.unwl%s+(.+)$")
                raw = normalizePlayerInput(raw)
                if not raw then
                    sendMessage("Usage: .unwl \"username\"")
                    return
                end
                local target = findPlayerByPartial(raw)
                if not target then
                    sendMessage("Could not find " .. raw .. " to unwhitelist")
                    return
                end
                if target.Name == Owner then
                    sendMessage("Cannot unwhitelist the owner")
                    return
                end
                whitelistedUsers[target.Name] = nil
                activeListeners[target.UserId] = nil
                disconnectPlayerChatRelay(target.UserId)
                sendMessage("Disallowed " .. target.Name .. " from using your stand")
            end
        end
    end
end

connectFastChatDispatch()

for _, player in pairs(Players:GetPlayers()) do
    if isAuthorized(player) then
        whitelistedUsers[player.Name] = true
        setupChatListener(player)
    end
end

Players.PlayerAdded:Connect(function(player)
    if isAuthorized(player) then
        setupChatListener(player)
    end
end)

Players.PlayerRemoving:Connect(function(player)
    activeListeners[player.UserId] = nil
    disconnectPlayerChatRelay(player.UserId)
end)

Players = game:GetService("Players")
LocalPlayer = game:GetService("Players").LocalPlayer
lockedTargetUserId = nil
autoLocked = false
sentrytarget = nil

function resetStandHome()
    if getgenv().enabled and standHomeName then
        startFollowingTarget(standHomeName)
    end
    teleporting = false
    voiding = false
end

handleStand2Command = function(rawInput)
    local target = findPlayerByPartial(rawInput)
    if not standHomeName then
        standHomeName = Owner
    end

    stand2Active = true
    stand2TargetName = rawInput
    stand2CurrentTarget = target
    stand2TargetUserId = target and target.UserId or nil
    lockedTarget = nil
    lockedTargetUserId = nil
    stomponly = false
    bringonly = false
    takeonly = false
    getgenv().downonly = false
    opkill = false
    flingonly = false
    killall = false
    summonTarget = nil
    shouldSwitch = false
    voiding = false
    teleporting = false
    getgenv().enabled = true
    startFollowingTarget(standHomeName)
    reloadTool()

    if target then
        lockedTarget = target
        lockedTargetUserId = target.UserId
        autoLocked = false
        voiding = false
        teleporting = true
        sendMessage("stand2 locked on " .. target.Name)
    else
        sendMessage("stand2 armed for " .. rawInput .. " (waiting)")
        resetStandHome()
    end
end

disableStand2 = function()
    if not stand2Active then
        return
    end
    local previousTarget = stand2CurrentTarget
    local previousId = stand2TargetUserId

    stand2Active = false
    stand2TargetName = nil
    stand2TargetUserId = nil
    stand2CurrentTarget = nil

    if lockedTarget and (lockedTarget == previousTarget or (previousId and lockedTarget.UserId == previousId)) then
        lockedTarget = nil
        lockedTargetUserId = nil
    end

    autoLocked = false
    resetStandHome()
    sendMessage("stand2 off")
end

task.spawn(function()
    while true do
        if hardStop then
            task.wait(standWait(perf.target))
            continue
        end
        -- If we are in a loop mode (.l / .lk) and current target is invalid/dead, keep re-acquiring
        if #ragebottargets > 0 then
            if not lockedTarget or not isValidLoopTarget(lockedTarget) then
                shouldSwitch = true
            end
        end

        if shouldSwitch and #ragebottargets > 0 then
            local attempts = 0
            local found = nil
            while attempts < #ragebottargets do
                currentTargetIndex = (currentTargetIndex % #ragebottargets) + 1
                local candidate = ragebottargets[currentTargetIndex]
                if isValidLoopTarget(candidate) then
                    found = candidate
                    break
                end
                attempts += 1
            end

            -- For .lk (single target), keep trying to re-find the same user by UserId/name if they respawn.
            if not found and #ragebottargets == 1 then
                local only = ragebottargets[1]
                local uid = only and only.UserId
                if uid then
                    for _, p in ipairs(Players:GetPlayers()) do
                        if p.UserId == uid and isValidLoopTarget(p) then
                            ragebottargets[1] = p
                            found = p
                            break
                        end
                    end
                end
            end

            if found then
                lockedTarget = found
                lockedTargetUserId = found.UserId
                autoLocked = false
                teleporting = true
                voiding = false
            else
                -- Nobody valid right now; keep trying in future ticks
                lockedTarget = nil
                teleporting = false
                voiding = true
            end
            shouldSwitch = false
        end

        -- Existing auto-relock by UserId
        if not lockedTarget and lockedTargetUserId and not autoLocked then
            for _, player in ipairs(Players:GetPlayers()) do
                if player.UserId == lockedTargetUserId then
                    lockedTarget = player
                    autoLocked = true
                    break
                end
            end
        end

        if lockedTarget then
            local targetCharacter = lockedTarget.Character
            if targetCharacter then
                local bodyEffects = targetCharacter:FindFirstChild("BodyEffects")
                local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                if isKO and trashtalkactive then
                    hasSentKOMessage = true
                else
                    hasSentKOMessage = false
                end
            end
            if not lockedTarget:IsDescendantOf(game) then
                lockedTargetUserId = lockedTarget.UserId
                lockedTarget = nil
                autoLocked = false
                if stand2Active then
                    resetStandHome()
                else
                    -- If we are looping, keep trying to reacquire; otherwise go idle
                    if #ragebottargets > 0 then
                        shouldSwitch = true
                    else
                        voiding = true
                    end
                end
            end
        end
        task.wait(standWait(perf.target))
    end
end)

task.spawn(function()
    while true do
        if stand2Active then
            local target = stand2CurrentTarget

            if not target or not target:IsDescendantOf(game) then
                local found = nil
                if stand2TargetUserId then
                    for _, plr in ipairs(Players:GetPlayers()) do
                        if plr.UserId == stand2TargetUserId then
                            found = plr
                            break
                        end
                    end
                end
                if not found and stand2TargetName then
                    found = findPlayerByPartial(stand2TargetName)
                end

                if found then
                    stand2CurrentTarget = found
                    lockedTarget = found
                    lockedTargetUserId = found.UserId
                    autoLocked = false
                    voiding = false
                    teleporting = true
                else
                    stand2CurrentTarget = nil
                    lockedTarget = nil
                    lockedTargetUserId = stand2TargetUserId
                    resetStandHome()
                end
            else
                if lockedTarget ~= target then
                    lockedTarget = target
                    lockedTargetUserId = target.UserId
                    autoLocked = false
                end
                local tChar = target.Character
                local tBody = tChar and tChar:FindFirstChild("BodyEffects")
                local tHumanoid = tChar and tChar:FindFirstChildOfClass("Humanoid")
                local sDeath = tBody and tBody:FindFirstChild("SDeath") and tBody["SDeath"].Value
                local dead = tHumanoid and tHumanoid.Health <= 0
                if sDeath or dead then
                    stand2CurrentTarget = nil
                    lockedTarget = nil
                    teleporting = false
                    resetStandHome()
                end
            end
        end
        task.wait(standWait(perf.target))
    end
end)

local function clampVelocitySample(velocity, maxVelocityOverride)
    local maxVelocity = maxVelocityOverride or combatConfig.maxVelocitySample or 450
    local magnitude = velocity.Magnitude
    if magnitude > maxVelocity and magnitude > 0 then
        return velocity.Unit * maxVelocity
    end
    return velocity
end

local function updateTargetVelocity(targetHRP)
    local now = os.clock()
    local deltaTime = math.max(now - followState.lastUpdate, 1 / 240)
    local targetPos = targetHRP.Position

    local sampledVelocity = Vector3.zero
    if followState.lastTargetPosition then
        sampledVelocity = (targetPos - followState.lastTargetPosition) / deltaTime
    end
    local partVelocity = targetHRP.AssemblyLinearVelocity or targetHRP.Velocity or Vector3.zero
    local rawSampleSpeed = sampledVelocity.Magnitude
    local rawPartSpeed = partVelocity.Magnitude
    local duelThreshold = combatConfig.standDuelTargetSpeedThreshold or (combatConfig.fastTargetSpeedThreshold or 85)
    local duelExtremeThreshold = combatConfig.standDuelExtremeSpeedThreshold or (combatConfig.extremeTargetSpeedThreshold or duelThreshold * 2)
    local duelSampleCap = math.max(combatConfig.standDuelVelocitySample or 0, combatConfig.maxVelocitySample or 0, 450)
    local standDuelTarget = math.max(rawSampleSpeed, rawPartSpeed) >= duelThreshold
    local standDuelExtreme = math.max(rawSampleSpeed, rawPartSpeed) >= duelExtremeThreshold

    sampledVelocity = clampVelocitySample(sampledVelocity, standDuelTarget and duelSampleCap or nil)
    partVelocity = clampVelocitySample(partVelocity, standDuelTarget and duelSampleCap or nil)

    local blend = clamp(
        standDuelTarget and (combatConfig.standDuelVelocityBlend or combatConfig.velocityBlend or 0.55)
            or (combatConfig.velocityBlend or 0.55),
        0,
        1
    )
    local mergedVelocity = sampledVelocity + (partVelocity - sampledVelocity) * blend
    local mergedSpeed = mergedVelocity.Magnitude
    local fastThreshold = combatConfig.fastTargetSpeedThreshold or 85
    local extremeThreshold = combatConfig.extremeTargetSpeedThreshold or (fastThreshold * 2)

    if (not followState.lastTargetPosition) or deltaTime > 0.25 then
        followState.targetVelocity = mergedVelocity
    else
        local smoothBase = combatConfig.velocitySmoothing or 0.5
        if mergedSpeed >= fastThreshold then
            smoothBase = math.max(smoothBase, combatConfig.fastVelocitySmoothing or 0.85)
        end
        if mergedSpeed >= extremeThreshold then
            smoothBase = math.max(smoothBase, 0.95)
        end
        if standDuelTarget then
            smoothBase = math.max(smoothBase, combatConfig.standDuelVelocitySmoothing or 0.96)
        end
        if standDuelExtreme then
            smoothBase = math.max(smoothBase, combatConfig.standDuelExtremeVelocitySmoothing or 0.99)
        end
        local smoothAlpha = clamp(smoothBase + math.min(deltaTime * 2, 0.35), 0.12, 1)
        followState.targetVelocity = followState.targetVelocity + (mergedVelocity - followState.targetVelocity) * smoothAlpha
    end

    followState.lastTargetPosition = targetPos
    followState.lastUpdate = now
    followState.standDuelTarget = standDuelTarget
    followState.standDuelExtreme = standDuelExtreme
    return targetPos, deltaTime
end

local function getOrbitAltitude(distance)
    if distance <= combatConfig.longRangeOrbitTrigger then
        return 1.2
    end
    return clamp(distance * 0.12, 1.2, combatConfig.longRangeOrbitHeight)
end

local indoorLoopState = {
    targetId = nil,
    lastCheck = 0,
    indoors = false,
    roofDistance = nil,
}
local loopBuildingTargetId = nil
local loopBuildingCheckTime = 0
local loopIsInBuilding = false
local loopBlockedSightUntil = 0
local loopAimMotionState = {
    targetId = nil,
    lastAt = 0,
}

local function isLikelyIndoors(targetHRP, targetCharacter)
    if not (targetHRP and targetCharacter) then
        return false, nil
    end

    local lp = game.Players.LocalPlayer
    local ignore = {}
    table.insert(ignore, targetCharacter)
    if lp and lp.Character then
        table.insert(ignore, lp.Character)
    end

    local params = RaycastParams.new()
    params.FilterType = Enum.RaycastFilterType.Blacklist
    params.IgnoreWater = true
    params.FilterDescendantsInstances = ignore

    local roofOrigin = targetHRP.Position + Vector3.new(0, 2.5, 0)
    local roofResult = workspace:Raycast(roofOrigin, Vector3.new(0, combatConfig.indoorRoofCheckDistance, 0), params)
    if not roofResult or not roofResult.Instance or not roofResult.Instance:IsA("BasePart") then
        return false, nil
    end
    if not roofResult.Instance.CanCollide then
        return false, nil
    end
    local roofDistance = (roofResult.Position - roofOrigin).Magnitude
    if roofDistance > combatConfig.indoorRoofMaxDistance then
        return false, nil
    end

    local wallOrigin = targetHRP.Position + Vector3.new(0, 2.5, 0)
    local directions = {
        Vector3.new(1, 0, 0),
        Vector3.new(-1, 0, 0),
        Vector3.new(0, 0, 1),
        Vector3.new(0, 0, -1),
    }
    local wallHits = 0
    for _, dir in ipairs(directions) do
        local result = workspace:Raycast(wallOrigin, dir * combatConfig.indoorWallCheckDistance, params)
        if result and result.Instance and result.Instance:IsA("BasePart") and result.Instance.CanCollide then
            wallHits += 1
            if wallHits >= combatConfig.indoorWallHitThreshold then
                return true, roofDistance
            end
        end
    end

    return false, nil
end

local function getLoopIndoors(loopTarget)
    if not (loopTarget and loopTarget.Character) then
        indoorLoopState.targetId = nil
        indoorLoopState.lastCheck = 0
        indoorLoopState.indoors = false
        indoorLoopState.roofDistance = nil
        return false
    end

    local now = os.clock()
    if indoorLoopState.targetId ~= loopTarget.UserId then
        indoorLoopState.targetId = loopTarget.UserId
        indoorLoopState.lastCheck = 0
        indoorLoopState.indoors = false
        indoorLoopState.roofDistance = nil
    end

    if (now - indoorLoopState.lastCheck) < combatConfig.indoorCheckInterval then
        return indoorLoopState.indoors
    end
    indoorLoopState.lastCheck = now

    local tChar = loopTarget.Character
    local tHRP = tChar and tChar:FindFirstChild("HumanoidRootPart")
    local indoors, roofDistance = isLikelyIndoors(tHRP, tChar)
    indoorLoopState.indoors = indoors
    indoorLoopState.roofDistance = roofDistance
    return indoorLoopState.indoors
end

local noise = math.noise or function()
    return 0
end

local function getStandEvasionFactor()
    local since = os.clock() - (standLastHitAt or -1e9)
    local duration = standEvasionSeconds or 2.8
    if since < 0 or since >= duration then
        return 0
    end
    return 1 - (since / duration)
end

local function applySkyCombatClamp(desiredPosition, targetHRP)
    if not desiredPosition or not targetHRP then
        return desiredPosition
    end
    local flameTargetHRP = lockedTarget and lockedTarget.Character and lockedTarget.Character:FindFirstChild("HumanoidRootPart")
    local flameCloseActive = flameModeActive
        and flameModeTargetUserId
        and lockedTarget
        and lockedTarget.UserId == flameModeTargetUserId
        and flameTargetHRP == targetHRP
    -- Do not force sky height when we need to grab/carry or use close flame pressure.
    if bringonly or takeonly or flameCloseActive then
        return desiredPosition
    end
    local minY = targetHRP.Position.Y + (combatConfig.skyCombatMinHeight or 0)
    if combatConfig.skyCombatMinAbsY then
        minY = math.max(minY, combatConfig.skyCombatMinAbsY)
    end
    if desiredPosition.Y < minY then
        return Vector3.new(desiredPosition.X, minY, desiredPosition.Z)
    end
    return desiredPosition
end

function isCalmStandCommandActive()
    return not vehicleMode
        and (
            smiteCommandInProgress
            or teleporting
            or bringonly
            or takeonly
            or toDeliveryActive
            or flameModeActive
            or stomponly
            or getgenv().downonly
            or opkill
            or killall
            or flingonly
            or lockedTarget ~= nil
            or sentrytarget ~= nil
            or #ragebottargets > 0
        )
end

local function applyStandMovementCFrame(playerHRP, cf)
    if not (playerHRP and cf) then
        return
    end
    addMovementPressure(1)
    playerHRP.CFrame = cf
    resetPartVelocity(playerHRP)
end

local function applyLoopStrafeAimMovement(playerHRP, targetHRP, aimPosition, targetIndoors, targetId, circleMode, calmBodyMode)
    if not (playerHRP and targetHRP and aimPosition) then
        return
    end

    local now = os.clock()
    if loopAimMotionState.targetId ~= targetId then
        loopAimMotionState.targetId = targetId
        loopAimMotionState.lastAt = now
    end

    local deltaTime = clamp(now - (loopAimMotionState.lastAt or now), 1 / 240, 0.08)
    loopAimMotionState.lastAt = now

    local targetPos = targetHRP.Position
    local flatOffset = Vector3.new(
        playerHRP.Position.X - targetPos.X,
        0,
        playerHRP.Position.Z - targetPos.Z
    )
    if flatOffset.Magnitude <= 0.1 then
        local fallbackLook = targetHRP.CFrame.LookVector
        flatOffset = Vector3.new(fallbackLook.X, 0, fallbackLook.Z)
        if flatOffset.Magnitude <= 0.1 then
            flatOffset = Vector3.new(1, 0, 0)
        end
    end

    local radial = flatOffset.Unit
    local tangent = Vector3.new(-radial.Z, 0, radial.X)
    if tangent.Magnitude <= 0.1 then
        tangent = Vector3.new(0, 0, 1)
    else
        tangent = tangent.Unit
    end

    local desiredRadius
    local desiredHeight
    local strafeDistance

    local sentryProfile = circleMode == "sentry"
    local attackProfile = circleMode == "attack"
    local indoorProfile = circleMode == "indoor"
    local forceGroundCircle = sentryProfile or attackProfile or indoorProfile

    if targetIndoors or forceGroundCircle then
        local circleRadius
        local circleSpeed
        local circleHeight
        local circleHeightBob
        local bobSpeed

        if sentryProfile then
            circleRadius = combatConfig.sentryCircleRadius or combatConfig.attackCircleRadius or combatConfig.indoorCircleRadius or combatConfig.indoorOrbitRadius or 16
            circleSpeed = combatConfig.sentryCircleStrafeSpeed or combatConfig.attackCircleStrafeSpeed or combatConfig.indoorCircleStrafeSpeed or combatConfig.indoorOrbitSpeed or 220
            circleHeight = combatConfig.sentryCircleHeight or combatConfig.attackCircleHeight or combatConfig.indoorCircleHeight or combatConfig.indoorLoopBaseHeight or 5
            circleHeightBob = combatConfig.sentryCircleHeightBob or combatConfig.attackCircleHeightBob or 0.8
            bobSpeed = (combatConfig.indoorOrbitSpeed or 90) * 0.28
        elseif attackProfile then
            circleRadius = combatConfig.attackCircleRadius or combatConfig.indoorCircleRadius or combatConfig.indoorOrbitRadius or 16
            circleSpeed = combatConfig.attackCircleStrafeSpeed or combatConfig.indoorCircleStrafeSpeed or combatConfig.indoorOrbitSpeed or 220
            circleHeight = combatConfig.attackCircleHeight or combatConfig.indoorCircleHeight or combatConfig.indoorLoopBaseHeight or 5
            circleHeightBob = combatConfig.attackCircleHeightBob or 0.18
            bobSpeed = (combatConfig.indoorOrbitSpeed or 90) * 0.22
        else
            circleRadius = combatConfig.indoorCircleRadius or combatConfig.indoorOrbitRadius or 16
            circleSpeed = combatConfig.indoorCircleStrafeSpeed or combatConfig.indoorOrbitSpeed or 220
            circleHeight = combatConfig.indoorCircleHeight or combatConfig.indoorLoopBaseHeight or 5
            circleHeightBob = combatConfig.indoorLoopHeightBob or 1.2
            bobSpeed = (combatConfig.indoorOrbitSpeed or 90) * 0.18
        end

        desiredRadius = circleRadius
        strafeDistance = circleSpeed * deltaTime
        local indoorBob = calmBodyMode and 0 or (math.sin(now * bobSpeed) * circleHeightBob)
        desiredHeight = targetPos.Y + circleHeight + indoorBob
        local roofDistance = indoorLoopState.roofDistance
        if targetIndoors and roofDistance then
            local roofOriginY = targetHRP.Position.Y + 2.5
            local maxY = (roofOriginY + roofDistance) - combatConfig.indoorOrbitCeilingMargin
            desiredHeight = math.min(desiredHeight, maxY)
        end
        local minCircleLift = sentryProfile and 2.6 or (attackProfile and 3.0 or 3.2)
        desiredHeight = math.max(targetPos.Y + minCircleLift, desiredHeight)
    else
        local loopMinRange = combatConfig.loopMinRange or 220
        local loopMaxRange = combatConfig.loopMaxRange or 520
        local currentRadius = flatOffset.Magnitude
        local preferredRadius = combatConfig.loopPreferredRange or currentRadius
        desiredRadius = clamp(
            currentRadius + (preferredRadius - currentRadius) * (combatConfig.loopSkyStrafeRadiusPull or 0.18),
            loopMinRange,
            loopMaxRange
        )
        strafeDistance = (combatConfig.loopSkyStrafeSpeed or combatConfig.loopOrbitSpeed or 320) * deltaTime
        local minSkyY = targetPos.Y + (combatConfig.skyCombatMinHeight or 0)
        if combatConfig.skyCombatMinAbsY then
            minSkyY = math.max(minSkyY, combatConfig.skyCombatMinAbsY)
        end
        local skyBob = calmBodyMode and 0 or (math.sin(now * ((combatConfig.loopOrbitSpeed or 90) * 0.12)) * (combatConfig.loopSkyStrafeHeightBob or 1.8))
        desiredHeight = math.max(playerHRP.Position.Y + skyBob, minSkyY)
    end

    local movedOffset = flatOffset + tangent * strafeDistance
    if movedOffset.Magnitude <= 0.1 then
        movedOffset = radial * desiredRadius
    else
        movedOffset = movedOffset.Unit * desiredRadius
    end

    local nextPosition = targetPos + movedOffset + Vector3.new(0, desiredHeight - targetPos.Y, 0)
    if not targetIndoors and not forceGroundCircle then
        nextPosition = applySkyCombatClamp(nextPosition, targetHRP)
    end

    applyStandMovementCFrame(playerHRP, CFrame.lookAt(nextPosition, aimPosition))
end

local calculateLeadAim

local function chaseTargetSmoothly(targetHRP, playerHRP, targetPos, deltaTime, aggressive)
    local calmBodyMode = isCalmStandCommandActive()
    local lockedTargetCombatMode = lockedTarget
        and lockedTarget.Character
        and lockedTarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP
    local loopModeActive = #ragebottargets > 0
        and lockedTarget
        and lockedTarget.Character
        and lockedTarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP
    local flameCloseMode = flameModeActive
        and flameModeTargetUserId
        and lockedTarget
        and lockedTarget.UserId == flameModeTargetUserId
        and lockedTarget.Character
        and lockedTarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP
    local sentryCircleMode = sentrytarget
        and sentrytarget.Character
        and sentrytarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP
    local loopTargetIndoors = loopModeActive and getLoopIndoors(lockedTarget) or false
    local sentryTargetIndoors = sentryCircleMode and getLoopIndoors(sentrytarget) or false
    local circleCombatMode = not bringonly
        and not takeonly
        and not flingonly
        and not flameCloseMode
        and (lockedTargetCombatMode or sentryCircleMode)
    local circleCombatTarget = sentryCircleMode and sentrytarget or lockedTarget
    local directAttackMode = circleCombatMode and not sentryCircleMode
    local circleTargetIndoors = sentryCircleMode
        and sentryTargetIndoors
        or (loopModeActive and loopTargetIndoors or (circleCombatTarget and getLoopIndoors(circleCombatTarget) or false))
    local liveTargetVelocity = targetHRP.AssemblyLinearVelocity or targetHRP.Velocity or Vector3.zero
    local standDuelTarget = followState.standDuelTarget
        and not bringonly
        and not takeonly
        and not flingonly
        and (lockedTargetCombatMode or loopModeActive or sentryCircleMode)
    local standDuelExtreme = standDuelTarget and followState.standDuelExtreme
    local duelBlend = standDuelTarget and 0.82 or 0.45
    local targetVelocity = followState.targetVelocity + (liveTargetVelocity - followState.targetVelocity) * duelBlend
    if standDuelTarget and liveTargetVelocity.Magnitude > targetVelocity.Magnitude then
        targetVelocity = liveTargetVelocity
    end
    local targetSpeed = targetVelocity.Magnitude
    local fastTargetThreshold = combatConfig.fastTargetSpeedThreshold or 85
    local extremeTargetThreshold = combatConfig.extremeTargetSpeedThreshold or (fastTargetThreshold * 2)
    local fastTarget = targetSpeed >= fastTargetThreshold
    local extremeTarget = targetSpeed >= extremeTargetThreshold
    local predictionTime = clamp(0.2 + math.min(targetSpeed * 0.02, 0.45), 0.16, 0.65)
    if loopModeActive then
        predictionTime = predictionTime + 0.14
    elseif directAttackMode then
        predictionTime = predictionTime + (combatConfig.attackPredictionBoost or 0.1)
    end
    if fastTarget then
        predictionTime = predictionTime + (combatConfig.fastTargetPredictionBoost or 0.3)
    end
    if extremeTarget then
        predictionTime = predictionTime + (combatConfig.extremeTargetPredictionBoost or 0.6)
    end
    if standDuelTarget then
        predictionTime = predictionTime + (combatConfig.standDuelPredictionBoost or 0.35)
    end
    if standDuelExtreme then
        predictionTime = predictionTime + (combatConfig.standDuelExtremePredictionBoost or 0.55)
    end
    local predictionMax = directAttackMode
        and (combatConfig.attackLeadTimeMax or combatConfig.leadTimeMax or 1.2)
        or (combatConfig.loopLeadTimeMax or 1.2)
    if standDuelTarget and directAttackMode then
        predictionMax = math.max(predictionMax, (combatConfig.attackLeadTimeMax or predictionMax) + (combatConfig.standDuelAttackLeadTimeBoost or 0.16))
    elseif standDuelTarget then
        predictionMax = math.max(predictionMax, (combatConfig.loopLeadTimeMax or predictionMax) + (combatConfig.standDuelLoopLeadTimeBoost or 0.35))
    end
    predictionTime = clamp(predictionTime, combatConfig.leadTimeMin or 0.12, predictionMax)
    local predictedPos = targetPos + targetVelocity * predictionTime
    local distanceToTarget = (targetPos - playerHRP.Position).Magnitude
    local minRange = combatConfig.minRange
    local preferredRange = combatConfig.preferredRange
    local maxRange = combatConfig.maxRange
    if directAttackMode then
        preferredRange = combatConfig.attackPreferredRange or preferredRange
        maxRange = combatConfig.attackMaxRange or math.max(maxRange, preferredRange)
    end
    if flameCloseMode then
        minRange = 2.8
        preferredRange = 3.8
        maxRange = 36
    end

    local desiredDistance = preferredRange
    local grabMode = bringonly or takeonly
    if distanceToTarget > maxRange then
        desiredDistance = math.max(preferredRange, maxRange * 0.88)
    elseif distanceToTarget < minRange then
        desiredDistance = minRange + 3
    end
    if grabMode then
        desiredDistance = math.min(desiredDistance, 8)
    end
    if flameCloseMode then
        desiredDistance = 3.5
    end

    local directionFromTarget
    local difference = playerHRP.Position - targetPos
    if difference.Magnitude > 0.1 then
        directionFromTarget = difference.Unit
    else
        directionFromTarget = -targetHRP.CFrame.LookVector
    end

    local altitude = getOrbitAltitude(distanceToTarget)
    if flameCloseMode then
        altitude = 0.1
    end
    if aggressive and #ragebottargets > 0 and lockedTarget and lockedTarget.Character and lockedTarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP then
        altitude = math.max(altitude, combatConfig.loopOrbitMinHeight)
    end
    local lateralDir = Vector3.new(-directionFromTarget.Z, 0, directionFromTarget.X)
    local orbitShift = lateralDir * (1.5 + (aggressive and 1.5 or math.cos(os.clock() * 1.6) * 1.2))
    if grabMode then
        orbitShift = Vector3.zero
    end
    if flameCloseMode then
        orbitShift = Vector3.zero
    end
    if calmBodyMode then
        orbitShift = Vector3.zero
    end
    local desiredPosition = predictedPos + directionFromTarget * desiredDistance + orbitShift + Vector3.new(0, altitude, 0)
    if flameCloseMode then
        local targetHead = targetHRP.Parent and targetHRP.Parent:FindFirstChild("Head")
        local headPos = targetHead and targetHead.Position or (targetHRP.Position + Vector3.new(0, 1.5, 0))
        local flameAngle = os.clock() * FLAME_ORBIT_SPEED
        local orbitOffset = Vector3.new(math.cos(flameAngle), 0, math.sin(flameAngle)) * FLAME_ORBIT_RADIUS
        local orbitCenter = targetHRP.Position + Vector3.new(0, 1.3, 0)
        desiredPosition = orbitCenter + orbitOffset + Vector3.new(0, FLAME_ORBIT_HEIGHT, 0)
        applyStandMovementCFrame(playerHRP, CFrame.lookAt(desiredPosition, headPos))
        return
    end

    local evasion = calmBodyMode and 0 or getStandEvasionFactor()
    if evasion > 0 then
        local now = os.clock()
        local jitterXZ = Vector3.new(
            noise(now * 5.2, 11.3, 0),
            0,
            noise(now * 5.2, -7.4, 0)
        ) * (1.4 + evasion * 3.2)
        local jitterY = noise(now * 5.6, 0, 9.1) * (0.8 + evasion * 1.4)
        if not grabMode then
            desiredPosition = desiredPosition + jitterXZ + Vector3.new(0, jitterY, 0)
        end
    end
    if circleCombatMode and circleCombatTarget then
        local circleAimPart = targetHRP.Parent and (targetHRP.Parent:FindFirstChild("Head") or targetHRP)
        local circleRangeRef = combatConfig.attackShootRange or combatConfig.maxRange
        local circleLeadTimeMax = combatConfig.attackLeadTimeMax or combatConfig.leadTimeMax
        local circleLeadScale = combatConfig.attackLeadScale or combatConfig.leadScale
        local circleProfile = sentryCircleMode and "sentry" or "attack"
        if loopModeActive then
            circleRangeRef = math.max(circleRangeRef, combatConfig.loopShootRange or circleRangeRef)
            circleLeadTimeMax = math.max(circleLeadTimeMax, combatConfig.loopLeadTimeMax or circleLeadTimeMax)
            circleLeadScale = math.max(circleLeadScale, combatConfig.loopLeadScale or circleLeadScale)
        end
        local circleAimPosition = circleAimPart and calculateLeadAim(
            playerHRP.Position,
            circleAimPart.Position,
            targetVelocity,
            distanceToTarget,
            circleRangeRef,
            circleLeadTimeMax,
            circleLeadScale
        ) or predictedPos
        applyLoopStrafeAimMovement(playerHRP, targetHRP, circleAimPosition, circleTargetIndoors, circleCombatTarget.UserId, circleProfile, calmBodyMode)
        return
    end
    desiredPosition = applySkyCombatClamp(desiredPosition, targetHRP)

    -- .l / .lk: always orbit the current loop target very fast (fly-like movement) - FAR AWAY IN SKY
    if loopModeActive then

        local now = os.clock()
        local currentLoopTargetId = lockedTarget and lockedTarget.UserId or nil
        if loopBuildingTargetId ~= currentLoopTargetId then
            loopBuildingTargetId = currentLoopTargetId
            loopBuildingCheckTime = 0
            loopIsInBuilding = false
            loopBlockedSightUntil = 0
        end
        local loopEvasion = calmBodyMode and 0 or math.max(evasion, 0.45)
        local orbitSpeed = combatConfig.loopOrbitSpeed * ((2.25 + loopEvasion * 1.55) * (standTuning.loopOrbitScale or 1))
        if fastTarget then
            local speedFactor = clamp((targetSpeed - fastTargetThreshold) / 120, 0, 0.9)
            orbitSpeed = orbitSpeed * (1 + speedFactor)
        end
        if extremeTarget then
            orbitSpeed = orbitSpeed * 1.12
        end
        if standDuelTarget then
            orbitSpeed = orbitSpeed * (combatConfig.standDuelLoopOrbitSpeedBoost or 1.24)
        end
        if standDuelExtreme then
            orbitSpeed = orbitSpeed * 1.08
        end
        local radiusJitter = 2.5 + loopEvasion * 6.8
        local isInBuilding = loopTargetIndoors or loopIsInBuilding
        if (not loopTargetIndoors) and (now - loopBuildingCheckTime) > 0.22 then
            loopBuildingCheckTime = now
            local rayOrigin = targetPos + Vector3.new(0, 5, 0)
            local rayDirection = Vector3.new(0, 1, 0)
            local raycastParams = RaycastParams.new()
            raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
            raycastParams.FilterDescendantsInstances = {lockedTarget.Character}
            local rayResult = workspace:Raycast(rayOrigin, rayDirection * 50, raycastParams)
            isInBuilding = rayResult ~= nil
            loopIsInBuilding = isInBuilding
        elseif loopTargetIndoors then
            loopIsInBuilding = true
            isInBuilding = true
        end

        local loopTargetCharacter = lockedTarget and lockedTarget.Character
        local loopTargetPart = loopTargetCharacter and (loopTargetCharacter:FindFirstChild("Head") or loopTargetCharacter:FindFirstChild("HumanoidRootPart"))
        local blockedSight = false
        if loopTargetCharacter and loopTargetPart then
            local sightDirection = loopTargetPart.Position - playerHRP.Position
            if sightDirection.Magnitude > 0.1 then
                local sightParams = RaycastParams.new()
                sightParams.FilterType = Enum.RaycastFilterType.Blacklist
                sightParams.IgnoreWater = true
                local sightFilter = {}
                if LocalPlayer and LocalPlayer.Character then
                    table.insert(sightFilter, LocalPlayer.Character)
                end
                sightParams.FilterDescendantsInstances = sightFilter
                local sightResult = workspace:Raycast(playerHRP.Position, sightDirection, sightParams)
                blockedSight = sightResult and sightResult.Instance and (not sightResult.Instance:IsDescendantOf(loopTargetCharacter)) or false
            end
        end
        if blockedSight then
            loopBlockedSightUntil = now + 1.2
            loopIsInBuilding = true
        end
        if now < loopBlockedSightUntil then
            isInBuilding = true
        end
        
        local orbitRadius
        local orbitHeight
        local orbitOffset
        local loopMinRange = combatConfig.loopMinRange or 220
        local loopPreferredRange = combatConfig.loopPreferredRange or (loopMinRange + 80)
        local loopMaxRange = combatConfig.loopMaxRange or (loopPreferredRange + 160)
        if fastTarget then
            loopPreferredRange = loopPreferredRange + 25
            loopMaxRange = loopMaxRange + 40
        end
        if extremeTarget then
            loopPreferredRange = loopPreferredRange + 35
            loopMaxRange = loopMaxRange + 55
        end
        if distanceToTarget < loopMinRange then
            local rangeGap = loopMinRange - distanceToTarget
            loopPreferredRange = math.min(loopMaxRange, loopPreferredRange + rangeGap * 0.9)
        end
        
        if isInBuilding then
            -- INDOOR CIRCLE: keep circling near target level so shots can connect through openings.
            local indoorSpeedBoost = combatConfig.indoorLoopSpeedBoost or 1.45
            if fastTarget then
                indoorSpeedBoost = indoorSpeedBoost + 0.12
            end
            if extremeTarget then
                indoorSpeedBoost = indoorSpeedBoost + 0.15
            end
            orbitSpeed = orbitSpeed * indoorSpeedBoost * (standTuning.indoorOrbitScale or 1)

            local indoorRadiusScale = combatConfig.indoorLoopRadiusScale or 1.1
            local indoorEvasionRadius = combatConfig.indoorLoopEvasionRadius or 2.5
            orbitRadius = (combatConfig.indoorOrbitRadius + loopEvasion * indoorEvasionRadius) * indoorRadiusScale
            if not calmBodyMode then
                orbitRadius = orbitRadius + (noise(now * 0.95, targetPos.X * 0.03, targetPos.Z * 0.03) * (0.8 + loopEvasion * 1.6))
            end
            orbitRadius = math.max(orbitRadius, combatConfig.indoorCircleRadius or combatConfig.indoorOrbitRadius or 14)
            local angle = now * orbitSpeed
            orbitOffset = Vector3.new(math.cos(angle), 0, math.sin(angle)) * orbitRadius
            local indoorBaseHeight = combatConfig.indoorLoopBaseHeight or 5
            local indoorHeightBob = combatConfig.indoorLoopHeightBob or 1.2
            orbitHeight = indoorBaseHeight + (calmBodyMode and 0 or (math.sin(now * 6.2) * indoorHeightBob))
            local roofDistance = indoorLoopState.roofDistance
            if roofDistance then
                local roofOriginY = targetHRP.Position.Y + 2.5
                local maxY = (roofOriginY + roofDistance) - combatConfig.indoorOrbitCeilingMargin
                local desiredY = predictedPos.Y + orbitHeight
                if desiredY > maxY then
                    orbitHeight = math.max(2.5, maxY - predictedPos.Y)
                end
            end
            orbitHeight = math.max(3.5, orbitHeight)
            desiredPosition = predictedPos + orbitOffset + Vector3.new(0, orbitHeight, 0)
        else
            -- SKY ORBIT: maintain aggressive long-range pressure while still tracking.
            orbitRadius = loopPreferredRange
                + (combatConfig.loopOrbitRadius * (0.12 + loopEvasion * 0.05))
            if not calmBodyMode then
                orbitRadius = orbitRadius + (noise(now * 0.85, targetPos.X * 0.03, targetPos.Z * 0.03) * radiusJitter)
            end
            orbitRadius = clamp(orbitRadius, loopMinRange, loopMaxRange)
            local angle = now * orbitSpeed
            orbitOffset = Vector3.new(math.cos(angle), 0, math.sin(angle)) * orbitRadius
            -- INCREASED HEIGHT: stand stays high in the sky
            local bob = 0
            if not calmBodyMode then
                bob = (math.sin(now * (8 + loopEvasion * 7)) * (1.2 + loopEvasion * 2.4))
                    + (noise(now * 2.1, 0, 0) * (0.9 + loopEvasion * 1.5))
            end
            orbitHeight = math.max(altitude, combatConfig.loopOrbitMinHeight) + bob + 50
            desiredPosition = predictedPos + orbitOffset + Vector3.new(0, orbitHeight, 0)
        end
        
        if not isInBuilding then
            desiredPosition = applySkyCombatClamp(desiredPosition, targetHRP)
        end
        applyStandMovementCFrame(playerHRP, CFrame.lookAt(desiredPosition, targetPos))
        
        -- MULTI-GUN FIRE: use all available guns for faster shooting
        if #ragebottargets > 0 and lockedTarget then
            local tools = collectGunTools()
            if #tools > 0 then
                local targetPart = lockedTarget.Character:FindFirstChild("Head") or lockedTarget.Character:FindFirstChild("HumanoidRootPart")
                if targetPart then
                    local targetVelocityLive = targetVelocity
                    local loopDistance = (targetPart.Position - playerHRP.Position).Magnitude
                    local loopLeadTimeMax = combatConfig.loopLeadTimeMax
                    local loopLeadScale = combatConfig.loopLeadScale
                    if fastTarget then
                        loopLeadTimeMax = loopLeadTimeMax + 0.2
                        loopLeadScale = loopLeadScale + 0.15
                    end
                    if extremeTarget then
                        loopLeadTimeMax = loopLeadTimeMax + 0.4
                        loopLeadScale = loopLeadScale + 0.25
                    end
                    if standDuelTarget then
                        loopLeadTimeMax = loopLeadTimeMax + (combatConfig.standDuelLoopLeadTimeBoost or 0.35)
                        loopLeadScale = loopLeadScale + (combatConfig.standDuelLoopLeadScaleBoost or 0.24)
                    end
                    if standDuelExtreme then
                        loopLeadTimeMax = loopLeadTimeMax + 0.15
                        loopLeadScale = loopLeadScale + 0.08
                    end
                    local loopAimPosition = calculateLeadAim(
                        playerHRP.Position,
                        targetPart.Position,
                        targetVelocityLive,
                        loopDistance,
                        combatConfig.loopShootRange,
                        loopLeadTimeMax,
                        loopLeadScale
                    )
                    local burstShots = combatConfig.loopShotsPerTick or 3
                    if fastTarget then
                        burstShots = math.max(burstShots, 4)
                    end
                    if extremeTarget then
                        burstShots = math.max(burstShots, 5)
                    end
                    burstShots = clamp(math.floor(burstShots + 0.5), 1, standTuning.maxBurstShots or 6)
                    for _, tool in ipairs(tools) do
                        fireToolAtTarget(tool, targetPart, burstShots, loopAimPosition)
                    end
                end
            end
        end
        
        return
    end

    -- If target is inside a building, orbit in a fast circle to keep pressure.
    local orbitTargetPlayer = nil
    if lockedTarget and lockedTarget.Character and lockedTarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP then
        orbitTargetPlayer = lockedTarget
    elseif sentrytarget and sentrytarget.Character and sentrytarget.Character:FindFirstChild("HumanoidRootPart") == targetHRP then
        orbitTargetPlayer = sentrytarget
    end

    if orbitTargetPlayer and getLoopIndoors(orbitTargetPlayer) then
        local now = os.clock()
        local orbitEvasion = calmBodyMode and 0 or math.max(evasion, 0.25)
        local orbitSpeed = combatConfig.indoorOrbitSpeed * (1 + orbitEvasion * 0.5)
        local orbitRadius = combatConfig.indoorOrbitRadius + orbitEvasion * 3
        if not calmBodyMode then
            orbitRadius = orbitRadius + (noise(now * 0.75, targetPos.X * 0.03, targetPos.Z * 0.03) * (0.8 + orbitEvasion * 2.8))
        end
        local angle = now * orbitSpeed
        local orbitOffset = Vector3.new(math.cos(angle), 0, math.sin(angle)) * orbitRadius
        local bob = 0
        if not calmBodyMode then
            bob = (math.sin(now * (6.5 + orbitEvasion * 4.5)) * (0.7 + orbitEvasion * 1.2))
                + (noise(now * 1.55, 0, 3.3) * (0.5 + orbitEvasion * 0.9))
        end
        local orbitHeight = math.max(altitude, combatConfig.indoorOrbitHeight, combatConfig.loopOrbitMinHeight) + bob
        local roofDistance = indoorLoopState.roofDistance
        if roofDistance then
            local roofOriginY = targetHRP.Position.Y + 2.5
            local maxY = (roofOriginY + roofDistance) - combatConfig.indoorOrbitCeilingMargin
            local desiredY = predictedPos.Y + orbitHeight
            if desiredY > maxY then
                orbitHeight = math.max(1, maxY - predictedPos.Y)
            end
        end
        desiredPosition = predictedPos + orbitOffset + Vector3.new(0, orbitHeight, 0)
        desiredPosition = applySkyCombatClamp(desiredPosition, targetHRP)
        applyStandMovementCFrame(playerHRP, CFrame.lookAt(desiredPosition, targetPos))
        return
    end

    if distanceToTarget < minRange and not aggressive then
        local retreatDir = (-directionFromTarget + Vector3.new(0, 0.2, 0))
        if retreatDir.Magnitude <= 0 then
            retreatDir = Vector3.new(0, 1, 0)
        end
        retreatDir = retreatDir.Unit
        desiredPosition = predictedPos + retreatDir * (minRange + 4) + lateralDir * 2 + Vector3.new(0, altitude + 3, 0)
    end

    desiredPosition = applySkyCombatClamp(desiredPosition, targetHRP)

    local toDesired = desiredPosition - playerHRP.Position
    local followSpeed = (14 + targetSpeed * 0.56 + distanceToTarget * 0.2) * (standTuning.movementScale or 1)
    if fastTarget and not grabMode then
        local followBoost = combatConfig.fastTargetFollowSpeedBoost or 1.65
        if extremeTarget then
            followBoost = followBoost * (combatConfig.extremeTargetFollowSpeedBoost or 1.35)
        end
        followSpeed = followSpeed * followBoost
    end
    if directAttackMode and not grabMode then
        local attackBoost = combatConfig.attackFollowSpeedBoost or 1.2
        if extremeTarget then
            attackBoost = attackBoost * (combatConfig.attackExtremeFollowSpeedBoost or 1.16)
        end
        followSpeed = followSpeed * attackBoost
    end
    if standDuelTarget and not grabMode then
        local duelFollowBoost = combatConfig.standDuelFollowSpeedBoost or 2.25
        if standDuelExtreme then
            duelFollowBoost = duelFollowBoost * (combatConfig.standDuelExtremeFollowSpeedBoost or 1.45)
        end
        followSpeed = followSpeed * duelFollowBoost
    end
    if grabMode then
        followSpeed = clamp((70 + distanceToTarget * 0.95) * 0.8, 60, 220)
    else
        local speedCap = fastTarget and 260 or 130
        if directAttackMode then
            speedCap = fastTarget and 340 or 220
        end
        if extremeTarget then
            speedCap = directAttackMode and 420 or 320
        end
        if standDuelTarget then
            speedCap = math.max(speedCap, combatConfig.standDuelSpeedCap or 420)
        end
        if standDuelExtreme then
            speedCap = math.max(speedCap, combatConfig.standDuelExtremeSpeedCap or 560)
        end
        followSpeed = clamp(followSpeed, 8, speedCap)
    end
    local maxStep = followSpeed * math.max(deltaTime, 0.02)
    if toDesired.Magnitude > 0 then
        local duelSnapDistance = combatConfig.standDuelSnapDistance or 24
        if aggressive or (standDuelTarget and toDesired.Magnitude >= duelSnapDistance) then
            applyStandMovementCFrame(playerHRP, CFrame.lookAt(desiredPosition, targetPos))
        else
            local step = math.min(toDesired.Magnitude, maxStep)
            local nextPosition = playerHRP.Position + toDesired.Unit * step
            applyStandMovementCFrame(playerHRP, CFrame.lookAt(nextPosition, targetPos))
        end
    else
        applyStandMovementCFrame(playerHRP, CFrame.lookAt(playerHRP.Position, targetPos))
    end
end

calculateLeadAim = function(origin, targetPosition, targetVelocity, distance, rangeRef, leadTimeMaxRef, leadScaleRef)
    local maxLeadTime = leadTimeMaxRef or combatConfig.leadTimeMax
    local travelTime = clamp(distance / combatConfig.bulletSpeed, 0.04, maxLeadTime)
    travelTime = clamp(travelTime + combatConfig.leadTimeMin, combatConfig.leadTimeMin, maxLeadTime)
    local rangeBase = math.max(rangeRef or combatConfig.maxRange, 1)
    local leadScale = leadScaleRef or combatConfig.leadScale
    local adaptiveScale = 1 + clamp(distance / rangeBase, 0, leadScale)
    local velocity = targetVelocity or Vector3.zero
    local lead = velocity * travelTime * adaptiveScale
    local fastThreshold = combatConfig.fastTargetSpeedThreshold or 85
    local speed = velocity.Magnitude
    if speed >= fastThreshold then
        local extraLead = clamp((speed - fastThreshold) / math.max(rangeBase * 0.22, 100), 0, 0.85)
        lead = lead * (1 + extraLead)
    end
    return targetPosition + lead
end

local function hasLineOfSight(origin, targetCharacter, aimPart)
    if not origin or not targetCharacter or not aimPart then
        return false
    end
    local direction = aimPart.Position - origin
    if direction.Magnitude <= 0.1 then
        return true
    end
    local params = RaycastParams.new()
    params.FilterType = Enum.RaycastFilterType.Blacklist
    params.IgnoreWater = true
    local filters = {}
    if LocalPlayer and LocalPlayer.Character then
        table.insert(filters, LocalPlayer.Character)
    end
    params.FilterDescendantsInstances = filters
    local result = workspace:Raycast(origin, direction, params)
    if not result then
        return true
    end
    local hit = result.Instance
    if not hit then
        return true
    end
    return hit:IsDescendantOf(targetCharacter)
end

task.spawn(function()
    while true do
        local followTarget = nil
        local targetIndoors = false
        if teleporting and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            if lockedTarget and lockedTarget.Character then
                followTarget = lockedTarget
            elseif sentrytarget and sentrytarget.Character then
                followTarget = sentrytarget
            end

            local targetCharacter = followTarget and followTarget.Character
            targetIndoors = followTarget and getLoopIndoors(followTarget) or false
            setNoclip(targetIndoors)

            local now = os.clock()
            local panicGhost = (now - (standLastHitAt or -1e9)) <= (standGhostPanicSeconds or 1.6)
            local commandGhost = teleporting
                and (lockedTarget or sentrytarget or (#ragebottargets > 0) or bringonly or stomponly or getgenv().downonly or opkill or flingonly or killall)
            local calmCommandGhost = isCalmStandCommandActive()
            setStandGhost((panicGhost or commandGhost or calmCommandGhost) and not vehicleMode and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress))

            if targetCharacter and LocalPlayer.Character then
                local targetHRP = targetCharacter:FindFirstChild("HumanoidRootPart")
                local playerHRP = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                local bodyEffects = targetCharacter:FindFirstChild("BodyEffects")
                local targetKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                local targetSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
                local targetId = followTarget and followTarget.UserId
                local targetCharacterChanged = targetCharacter ~= followState.currentTargetCharacter
                local targetKOState = targetKO and true or false
                local targetDeadState = targetSDeath and true or false
                local targetStateChanged = targetKOState ~= followState.lastTargetWasKO or targetDeadState ~= followState.lastTargetWasDead
                if targetId ~= followState.currentTargetId or targetCharacterChanged then
                    followState.currentTargetId = targetId
                    followState.currentTargetCharacter = targetCharacter
                    followState.lastTargetWasKO = targetKOState
                    followState.lastTargetWasDead = targetDeadState
                    resetFollowPrediction()
                    resetCombatFireWindow()
                    requestCombatAttackPrime(followTarget, true)
                elseif targetStateChanged then
                    local targetBecameAlive = (followState.lastTargetWasKO or followState.lastTargetWasDead) and not targetKOState and not targetDeadState
                    followState.currentTargetCharacter = targetCharacter
                    followState.lastTargetWasKO = targetKOState
                    followState.lastTargetWasDead = targetDeadState
                    if targetBecameAlive then
                        resetFollowPrediction()
                        resetCombatFireWindow()
                        reloadTool()
                        requestCombatAttackPrime(followTarget, true)
                    end
                end

                if getgenv().downonly and (targetKO or targetSDeath) then
                    teleporting = false
                    voiding = true
                elseif targetHRP and playerHRP then
                    -- Only enable teleporting once a valid destination has been assigned.
                    if gotoCFrame ~= nil or gotoTarget ~= nil or gotoTargetUserId ~= nil then
                        teleporting = true
                    else
                        teleporting = false
                    end
                    voiding = false
                    local targetPos, deltaTime = updateTargetVelocity(targetHRP)
                    local aggressiveFollow = stomponly or bringonly or getgenv().downonly or (#ragebottargets > 0)
                    chaseTargetSmoothly(targetHRP, playerHRP, targetPos, deltaTime, aggressiveFollow)
                else
                    followState.currentTargetId = nil
                    followState.currentTargetCharacter = nil
                    followState.lastTargetWasKO = nil
                    followState.lastTargetWasDead = nil
                    resetFollowPrediction()
                end
            else
                followState.currentTargetId = nil
                followState.currentTargetCharacter = nil
                followState.lastTargetWasKO = nil
                followState.lastTargetWasDead = nil
                resetFollowPrediction()
            end
        else
            setNoclip(false)
            setStandGhost(isCalmStandCommandActive() and not vehicleMode and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress))
            followState.currentTargetId = nil
            followState.currentTargetCharacter = nil
            followState.lastTargetWasKO = nil
            followState.lastTargetWasDead = nil
            resetFollowPrediction()
        end

        local teleportDelay = perf.teleport
        if (lockedTarget or sentrytarget) and perf.teleportCombat then
            teleportDelay = perf.teleportCombat
        end
        local minTeleportDelay = standTuning.minTeleportDelay or 0.006
        local attackFollowMinDelay = combatConfig.attackFollowMinDelay or minTeleportDelay
        local loopFollowMinDelay = combatConfig.loopFollowMinDelay or minTeleportDelay
        local standDuelFollowMinDelay = combatConfig.standDuelFollowMinDelay or attackFollowMinDelay
        local flameFastTrack = followTarget
            and flameModeActive
            and flameModeTargetUserId
            and followTarget.UserId == flameModeTargetUserId
        local duelFastTrack = followTarget
            and followState.standDuelTarget
            and not bringonly
            and not takeonly
            and not flingonly
        if followTarget and targetIndoors then
            teleportDelay = math.min(teleportDelay, minTeleportDelay)
        end
        if followTarget and followTarget == lockedTarget and #ragebottargets > 0 then
            teleportDelay = math.min(teleportDelay, loopFollowMinDelay)
        end
        if followTarget and not bringonly and not takeonly and not flingonly then
            if lockedTarget and followTarget == lockedTarget and #ragebottargets == 0 then
                teleportDelay = math.min(teleportDelay, attackFollowMinDelay)
            elseif sentrytarget and followTarget == sentrytarget then
                teleportDelay = math.min(teleportDelay, combatConfig.sentryFollowMinDelay or attackFollowMinDelay)
            end
        end
        if flameFastTrack then
            teleportDelay = math.min(teleportDelay, 0.01)
        end
        if duelFastTrack then
            teleportDelay = math.min(teleportDelay, standDuelFollowMinDelay)
        end
        teleportDelay = math.max(teleportDelay, math.min(minTeleportDelay, attackFollowMinDelay, loopFollowMinDelay))
        if followTarget or teleporting then
            teleportDelay = teleportDelay * getMovementDelayScale()
        end
        task.wait(standWait(teleportDelay))
    end
end)

canrun = true
Players = game:GetService("Players")
LocalPlayer = Players.LocalPlayer
char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
humanoid = char:WaitForChild("Humanoid")
rootPart = char:WaitForChild("HumanoidRootPart")

task.spawn(function()
    while true do
        -- Main combat loop: should run for ALL offensive modes (.d/.lk use downonly, etc.)
        if lockedTarget
            and not (flameModeActive and flameModeTargetUserId and lockedTarget.UserId == flameModeTargetUserId)
            and not bringonly
            and not takeonly
            and not opkill
            and not flingonly
            and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            local character = lockedTarget.Character
            local myCharacter = LocalPlayer.Character
            if character and myCharacter then
                local bodyEffects = character:FindFirstChild("BodyEffects")
                local myBodyEffects = myCharacter:FindFirstChild("BodyEffects")
                local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
                local isNil = not character:FindFirstChild("UpperTorso") or not character:FindFirstChild("Head")
                local isGrabbed = character:FindFirstChild("GRABBING_CONSTRAINT")
                local hasForceField = character:FindFirstChildOfClass("ForceField")
                local isReloading = myBodyEffects and myBodyEffects:FindFirstChild("Reload") and myBodyEffects["Reload"].Value
                if shouldTriggerAbuseProtection(myCharacter, character, isReloading) then
                    local humanoid = myCharacter:FindFirstChild("Humanoid")
                    if humanoid then
                        abuseProtectionCooldownUntil = os.clock() + ABUSE_PROTECTION_RETRY_DELAY
                        canrun = false
                        voiding = true
                        teleporting = false
                        task.wait(0.1)
                        humanoid.Health = 0
                        task.wait(0.1)
                        canrun = true
                    end
                end
                if (isSDeath or isNil) and not isReloading and canrun then
                    teleporting = false
                    voiding = true
                    reloadTool()
                    shouldSwitch = true
                    if not didRefreshOnDeath and fpactive then
                        didRefreshOnDeath = true
                        task.delay(0.2, function()
                            refreshingfakeposition = true
                            task.wait(3.65)
                            refreshingfakeposition = false
                        end)
                    end
                elseif isKO and not isSDeath and not isGrabbed and not isNil and not isReloading and canrun and not refreshingfakeposition then
                    if getgenv().downonly then
                        teleporting = false
                        voiding = true
                        reloadTool()
                        shouldSwitch = true
                    else
                        voiding = false
                        teleporting = false
                        local upperTorso = character:FindFirstChild("UpperTorso")
                        if upperTorso and LocalPlayer.Character then
                            local humanoidRootPart = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                            if humanoidRootPart then
                                humanoidRootPart.Velocity = Vector3.zero
                                humanoidRootPart.RotVelocity = Vector3.zero
                                humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
                                humanoidRootPart.AssemblyAngularVelocity = Vector3.zero
                                humanoidRootPart.CFrame = CFrame.new(upperTorso.Position + Vector3.new(0, 3.5, 0))
                                task.wait(0.1)
                            end
                        end
                    end
                elseif not isKO and not isSDeath and not hasForceField and not isGrabbed and not isNil and not isReloading and canrun and not refreshingfakeposition then
                    teleporting = true
                    voiding = false
                    didRefreshOnDeath = false
                elseif isReloading and not refreshingfakeposition then
                    teleporting = false
                    voiding = true
                elseif hasForceField and not isReloading and not refreshingfakeposition then
                    teleporting = false
                    voiding = true
                    reloadTool()
                end
            end
            -- Only stomp when explicitly in stomp mode.
            -- .lk (loopknock) should knock only, not stomp.
            if stomponly then
                ReplicatedStorage.MainEvent:FireServer("Stomp")
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

task.spawn(function()
    while true do
        if stomponly and not bringonly and not takeonly and not getgenv().downonly and not opkill and lockedTarget and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            local character = lockedTarget.Character
            if character then
                local bodyEffects = character:FindFirstChild("BodyEffects")
                local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value

                if isKO and not isSDeath then
                    teleporting = false
                    voiding = false
                    local upperTorso = character:FindFirstChild("UpperTorso")
                    if upperTorso and LocalPlayer.Character then
                        local humanoidRootPart = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                        if humanoidRootPart then
                            humanoidRootPart.Velocity = Vector3.zero
                            humanoidRootPart.RotVelocity = Vector3.zero
                            humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
                            humanoidRootPart.AssemblyAngularVelocity = Vector3.zero
                            humanoidRootPart.CFrame = CFrame.new(upperTorso.Position + Vector3.new(0, 3.5, 0))
                            task.wait(0.1)
                        end
                    end
                elseif isSDeath then
                    lockedTarget = nil
                    teleporting = false
                    voiding = true
                    reloadTool()
                elseif not isKO and not isSDeath then
                    teleporting = true
                    voiding = false
                end
            end
            -- Only stomp when explicitly in stomp mode.
            -- .lk (loopknock) should knock only, not stomp.
            if stomponly then
                ReplicatedStorage.MainEvent:FireServer("Stomp")
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

Players = game:GetService("Players")
LocalPlayer = Players.LocalPlayer
bringconnection = nil

task.spawn(function()
    while true do
        if hardStop then
            disconnectBringConnection()
            task.wait(standWait(perf.combat))
            continue
        end
        if not bringonly and bringconnection then
            disconnectBringConnection()
        end
        if bringonly and (not lockedTarget or not lockedTarget.Character) and bringconnection then
            disconnectBringConnection()
        end
        if bringonly and toDeliveryActive and (not lockedTarget or not lockedTarget.Character) then
            local ownerPlr = Players:FindFirstChild(Owner)
            if ownerPlr and ownerPlr.Character then
                lockedTarget = ownerPlr
            end
        end
        if bringonly and lockedTarget and lockedTarget.Character and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            local character = lockedTarget.Character

            local bodyEffects = character and character:FindFirstChild("BodyEffects")
            local ownerPlrForStrict = Players:FindFirstChild(Owner)
            local ownerCharForStrict = ownerPlrForStrict and ownerPlrForStrict.Character
            local activeGotoTarget = gotoTarget or pendingGotoTarget
            local activeGotoTargetUserId = gotoTargetUserId or pendingGotoTargetUserId or (activeGotoTarget and activeGotoTarget.UserId) or nil
            local hasActiveBringTarget = activeGotoTarget ~= nil or activeGotoTargetUserId ~= nil
            local strictDeliveryGrab = toDeliveryActive and ownerCharForStrict and character == ownerCharForStrict
            local ownerBringStrictMode = (not toDeliveryActive)
                and bringonly
                and commandSender == Owner
                and hasActiveBringTarget
                and gotoCFrame == nil
                and ownerPlrForStrict ~= nil
                and activeGotoTargetUserId == ownerPlrForStrict.UserId
            local fastBringCommand = (not toDeliveryActive) and hasActiveBringTarget and gotoCFrame == nil and not ownerBringStrictMode
            local strictCarryGrab = strictDeliveryGrab or ownerBringStrictMode or fastBringCommand
            local strictDropMode = strictDeliveryGrab or ownerBringStrictMode
            local function confirmBringGrab()
                if strictCarryGrab then
                    return isHoldingTargetForDelivery(character)
                end
                return isHoldingTarget(character)
            end

            local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
            local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value

            -- Only attempt to knock out the target while it is still not grabbed.
            if bringonly and not isKO and not isSDeath and not confirmBringGrab() then
                if tryForceBringKO(lockedTarget) then
                    bodyEffects = character and character:FindFirstChild("BodyEffects")
                    isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                    isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
                end
            end

            local grabbed = false

            local character = lockedTarget.Character
            local humanoidRootPart = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            local grabTargetPart = getGrabTargetPart(character)

            local nextBringTargetUserId = lockedTarget and lockedTarget.UserId or nil
            local nextBringDeliveryMode = not not toDeliveryActive
            if bringAttemptTargetUserId ~= nextBringTargetUserId or bringAttemptDeliveryMode ~= nextBringDeliveryMode then
                resetBringGrabAttemptState()
                bringAttemptTargetUserId = nextBringTargetUserId
                bringAttemptDeliveryMode = nextBringDeliveryMode
            end
            local currentBringRunId = bringRunId

            if bringconnection and (bringConnectionCharacter ~= character or bringConnectionRunId ~= currentBringRunId) then
                disconnectBringConnection()
            end
            if not bringconnection then
                bringConnectionCharacter = character
                bringConnectionRunId = currentBringRunId
                bringconnection = character.ChildAdded:Connect(function(child)
                    if child.Name == "GRABBING_CONSTRAINT" then
                        task.defer(function()
                            task.wait(0.05)
                            if currentBringRunId ~= bringRunId then
                                return
                            end
                            if confirmBringCarryWithRetry(
                                character,
                                confirmBringGrab,
                                ownerBringStrictMode or strictDeliveryGrab,
                                strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_ROUNDS or BRING_TARGET_GRAB_HARDLOCK_ROUNDS,
                                strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_OFFSETS or BRING_TARGET_GRAB_HARDLOCK_OFFSETS,
                                strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_SETTLE or BRING_TARGET_GRAB_HARDLOCK_SETTLE,
                                strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_RECHECK_WAIT or BRING_TARGET_GRAB_HARDLOCK_RECHECK_WAIT,
                                strictDeliveryGrab and DELIVERY_OWNER_GRAB_PART_NAMES or BRING_TARGET_GRAB_PART_NAMES
                            ) then
                                grabbed = true
                                lockGrabRemoteWindow()
                                disconnectBringConnection()
                            end
                        end)
                    end
                end)
            end

            if character:FindFirstChild("GRABBING_CONSTRAINT") then
                if confirmBringCarryWithRetry(
                    character,
                    confirmBringGrab,
                    ownerBringStrictMode or strictDeliveryGrab,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_ROUNDS or BRING_TARGET_GRAB_HARDLOCK_ROUNDS,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_OFFSETS or BRING_TARGET_GRAB_HARDLOCK_OFFSETS,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_SETTLE or BRING_TARGET_GRAB_HARDLOCK_SETTLE,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_RECHECK_WAIT or BRING_TARGET_GRAB_HARDLOCK_RECHECK_WAIT,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_PART_NAMES or BRING_TARGET_GRAB_PART_NAMES
                ) then
                    grabbed = true
                    lockGrabRemoteWindow()
                    disconnectBringConnection()
                end
            end

            if not grabbed and forceBringDrop and confirmBringGrab() then
                grabbed = true
                if strictDeliveryGrab then
                    local carriedHRP = character:FindFirstChild("HumanoidRootPart")
                        or character:FindFirstChild("UpperTorso")
                        or character:FindFirstChild("Torso")
                    local localHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                    if carriedHRP and localHRP then
                        placeCarriedBodyAtPosition(carriedHRP, localHRP.Position, true)
                        resetPartVelocity(carriedHRP)
                    end
                end
                forceBringDrop = false
            end

            if not grabbed and isKO and humanoidRootPart and grabTargetPart then
                teleporting = false
                voiding = false

                if ownerBringStrictMode then
                    local ownerBringLockParts = getGrabTargetParts(character, OWNER_BRING_GRAB_PART_NAMES)
                    local ownerBringLockPart = ownerBringLockParts[1] or grabTargetPart
                    if ownerBringLockPart and ownerBringLockPart.Parent then
                        local lockOffset = OWNER_BRING_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 1.95, 0)
                        local lockPos = ownerBringLockPart.Position + lockOffset
                        moveStandToCFrameExact(LocalPlayer.Character, humanoidRootPart, getNorthSouthGrabCFrame(lockPos))
                        task.wait(0.01)
                    end
                    grabbed = attemptReliableBringGrab(character, confirmBringGrab, OWNER_BRING_GRAB_HARDLOCK_ROUNDS, {
                        approachOffsets = OWNER_BRING_GRAB_HARDLOCK_OFFSETS,
                        settleTime = OWNER_BRING_GRAB_HARDLOCK_SETTLE,
                        recheckWait = OWNER_BRING_GRAB_HARDLOCK_RECHECK_WAIT,
                        targetPartNames = OWNER_BRING_GRAB_PART_NAMES,
                        orientNorthSouth = true,
                    })
                    if not grabbed and ownerBringLockPart and ownerBringLockPart.Parent then
                        local retryOffset = OWNER_BRING_GRAB_HARDLOCK_OFFSETS[2] or OWNER_BRING_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 1.72, 0)
                        local retryPos = ownerBringLockPart.Position + retryOffset
                        moveStandToCFrameExact(LocalPlayer.Character, humanoidRootPart, getNorthSouthGrabCFrame(retryPos))
                        task.wait(0.01)
                        grabbed = attemptReliableBringGrab(character, confirmBringGrab, OWNER_BRING_GRAB_HARDLOCK_ROUNDS, {
                            approachOffsets = OWNER_BRING_GRAB_HARDLOCK_OFFSETS,
                            settleTime = OWNER_BRING_GRAB_HARDLOCK_SETTLE,
                            recheckWait = OWNER_BRING_GRAB_HARDLOCK_RECHECK_WAIT,
                            targetPartNames = OWNER_BRING_GRAB_PART_NAMES,
                            orientNorthSouth = true,
                        })
                    end
                    if not grabbed then
                        grabbed = attemptReliableBringGrab(character, confirmBringGrab, OWNER_BRING_GRAB_ROUNDS, {
                            approachOffsets = OWNER_BRING_GRAB_APPROACH_OFFSETS,
                            settleTime = OWNER_BRING_GRAB_SETTLE,
                            recheckWait = OWNER_BRING_GRAB_RECHECK_WAIT,
                            targetPartNames = OWNER_BRING_GRAB_PART_NAMES,
                            orientNorthSouth = true,
                        })
                    end
                else
                    local grabRounds = strictDropMode and (GRAB_RETRY_ROUNDS + 1) or GRAB_RETRY_ROUNDS
                    local grabOptions = nil
                    if fastBringCommand then
                        grabRounds = math.max(grabRounds, BRING_TARGET_GRAB_ROUNDS, FAST_BRING_GRAB_ROUNDS)
                        grabOptions = {
                            approachOffsets = BRING_TARGET_GRAB_APPROACH_OFFSETS,
                            settleTime = BRING_TARGET_GRAB_SETTLE,
                            recheckWait = BRING_TARGET_GRAB_RECHECK_WAIT,
                            targetPartNames = BRING_TARGET_GRAB_PART_NAMES,
                        }
                    end
                    if strictDeliveryGrab then
                        grabRounds = math.max(grabRounds, DELIVERY_OWNER_GRAB_ROUNDS)
                        grabOptions = {
                            approachOffsets = DELIVERY_OWNER_GRAB_APPROACH_OFFSETS,
                            settleTime = DELIVERY_OWNER_GRAB_SETTLE,
                            recheckWait = DELIVERY_OWNER_GRAB_RECHECK_WAIT,
                            targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                            orientNorthSouth = true,
                        }
                    end
                    grabbed = attemptReliableBringGrab(character, confirmBringGrab, grabRounds, grabOptions)
                end
                if fastBringCommand and not grabbed then
                    local hardLockParts = getGrabTargetParts(character, BRING_TARGET_GRAB_PART_NAMES)
                    local hardLockPart = hardLockParts[1] or grabTargetPart
                    if hardLockPart and hardLockPart.Parent then
                        local lockOffset = BRING_TARGET_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 2.15, 0)
                        local lockPos = hardLockPart.Position + lockOffset
                        moveStandToCFrameExact(LocalPlayer.Character, humanoidRootPart, CFrame.lookAt(lockPos, hardLockPart.Position))
                        task.wait(0.03)
                    end
                    grabbed = attemptReliableBringGrab(character, confirmBringGrab, BRING_TARGET_GRAB_HARDLOCK_ROUNDS, {
                        approachOffsets = BRING_TARGET_GRAB_HARDLOCK_OFFSETS,
                        settleTime = BRING_TARGET_GRAB_HARDLOCK_SETTLE,
                        recheckWait = BRING_TARGET_GRAB_HARDLOCK_RECHECK_WAIT,
                        targetPartNames = BRING_TARGET_GRAB_PART_NAMES,
                    })
                end
                if strictDeliveryGrab and not grabbed then
                    local hardLockParts = getGrabTargetParts(character, DELIVERY_OWNER_GRAB_PART_NAMES)
                    local hardLockPart = hardLockParts[1] or grabTargetPart
                    if hardLockPart and hardLockPart.Parent then
                        local lockOffset = DELIVERY_OWNER_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 2.2, 0)
                        local lockPos = hardLockPart.Position + lockOffset
                        moveStandToCFrameExact(LocalPlayer.Character, humanoidRootPart, getNorthSouthGrabCFrame(lockPos))
                        task.wait(0.03)
                    end
                    grabbed = attemptReliableBringGrab(character, confirmBringGrab, DELIVERY_OWNER_GRAB_HARDLOCK_ROUNDS, {
                        approachOffsets = DELIVERY_OWNER_GRAB_HARDLOCK_OFFSETS,
                        settleTime = DELIVERY_OWNER_GRAB_HARDLOCK_SETTLE,
                        recheckWait = DELIVERY_OWNER_GRAB_HARDLOCK_RECHECK_WAIT,
                        targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                        orientNorthSouth = true,
                    })
                end
            elseif grabbed then
                -- Already grabbed, proceed to drop immediately
                teleporting = false
                voiding = false
            else
                teleporting = true
                voiding = false
            end

            if grabbed then
                if strictCarryGrab then
                    if not confirmBringGrab() then
                        grabbed = false
                    end
                elseif not confirmBringGrab() and not character:FindFirstChild("GRABBING_CONSTRAINT") then
                    grabbed = false
                end
                if grabbed and (fastBringCommand or ownerBringStrictMode or strictDeliveryGrab) and not confirmBringCarryWithRetry(
                    character,
                    confirmBringGrab,
                    ownerBringStrictMode or strictDeliveryGrab,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_ROUNDS or BRING_TARGET_GRAB_HARDLOCK_ROUNDS,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_OFFSETS or BRING_TARGET_GRAB_HARDLOCK_OFFSETS,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_SETTLE or BRING_TARGET_GRAB_HARDLOCK_SETTLE,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_HARDLOCK_RECHECK_WAIT or BRING_TARGET_GRAB_HARDLOCK_RECHECK_WAIT,
                    strictDeliveryGrab and DELIVERY_OWNER_GRAB_PART_NAMES or BRING_TARGET_GRAB_PART_NAMES
                ) then
                    grabbed = false
                    logDrop("bring attach confirmation failed after retry; keeping state clean")
                end
                if grabbed and strictDeliveryGrab then
                    local carriedHRP = character:FindFirstChild("HumanoidRootPart")
                        or character:FindFirstChild("UpperTorso")
                        or character:FindFirstChild("Torso")
                    local localHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                    if carriedHRP and localHRP then
                        placeCarriedBodyAtPosition(carriedHRP, localHRP.Position, true)
                        resetPartVelocity(carriedHRP)
                    end
                end
            end

            if grabbed then
                -- Assign any pending goto target once the target has been successfully grabbed.
                if gotoTarget == nil and (pendingGotoTarget ~= nil or pendingGotoTargetUserId ~= nil) then
                    gotoTarget = pendingGotoTarget or (pendingGotoTargetUserId and Players:GetPlayerByUserId(pendingGotoTargetUserId)) or nil
                    gotoTargetUserId = pendingGotoTargetUserId or (gotoTarget and gotoTarget.UserId) or nil
                    pendingGotoTarget = nil
                    pendingGotoTargetUserId = nil
                end

                local carriedCharacter = character
                lockedTarget = nil
                lockedTargetUserId = nil
                autoLocked = false
                local didDrop = false
                local fastBringDropValidated = false
                local strictDeliveryDropValidated = false
                local ownerBringDropValidated = false
                local dropBaseCFrame = nil
                local dropPreferDirect = false
                local dropDirectPosition = nil

                if (not gotoTarget) and gotoTargetUserId then
                    for _, plr in ipairs(Players:GetPlayers()) do
                        if plr.UserId == gotoTargetUserId then
                            gotoTarget = plr
                            break
                        end
                    end
                end

                if gotoCFrame then
                    dropBaseCFrame = gotoCFrame
                elseif gotoTarget and gotoTarget.Character then
                    local targetHRP = gotoTarget.Character:FindFirstChild("HumanoidRootPart")
                    if targetHRP then
                        dropBaseCFrame = CFrame.new(targetHRP.Position)
                        if toDeliveryActive then
                            lastToDropCFrame = dropBaseCFrame
                            dropPreferDirect = true
                        end
                        dropDirectPosition = targetHRP.Position
                        local indoors = false
                        -- Prefer a simple roof check for drop (more reliable than wall checks).
                        local params = RaycastParams.new()
                        params.FilterType = Enum.RaycastFilterType.Blacklist
                        params.IgnoreWater = true
                        local ignore = {}
                        local lp = game.Players.LocalPlayer
                        if lp and lp.Character then
                            table.insert(ignore, lp.Character)
                        end
                        table.insert(ignore, gotoTarget.Character)
                        params.FilterDescendantsInstances = ignore

                        local roofOrigin = targetHRP.Position + Vector3.new(0, 2.5, 0)
                        local roofResult = workspace:Raycast(roofOrigin, Vector3.new(0, combatConfig.indoorRoofCheckDistance, 0), params)
                        if roofResult and roofResult.Instance and roofResult.Instance:IsA("BasePart") and roofResult.Instance.CanCollide then
                            local roofDistance = (roofResult.Position - roofOrigin).Magnitude
                            if roofDistance <= combatConfig.indoorRoofMaxDistance then
                                indoors = true
                            end
                        end

                        if (not indoors) and isLikelyIndoors then
                            local ok, res = pcall(isLikelyIndoors, targetHRP, gotoTarget.Character)
                            indoors = ok and res or false
                        end

                        if indoors then
                            dropPreferDirect = true
                        end
                    end
                end

                if (not dropBaseCFrame) and (not toDeliveryActive) and commandSender then
                    local dropRecipient = Players:FindFirstChild(commandSender)
                    local dropRecipientHRP = dropRecipient and dropRecipient.Character and dropRecipient.Character:FindFirstChild("HumanoidRootPart")
                    if dropRecipientHRP then
                        dropBaseCFrame = CFrame.new(dropRecipientHRP.Position)
                        dropDirectPosition = dropRecipientHRP.Position
                    end
                end

                if (not dropBaseCFrame) and lastToDestination then
                    local resolved = locationCFrames[lastToDestination:lower()]
                    if resolved then
                        dropBaseCFrame = resolved
                        if toDeliveryActive then
                            lastToDropCFrame = resolved
                        end
                    else
                        local targetPlayer = resolveDeliveryTargetPlayer(lastToDestination)
                        if targetPlayer and targetPlayer.Character then
                            local targetHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                            if targetHRP then
                                dropBaseCFrame = CFrame.new(targetHRP.Position)
                                if toDeliveryActive then
                                    lastToDropCFrame = dropBaseCFrame
                                end
                                dropDirectPosition = targetHRP.Position
                                if toDeliveryActive then
                                    dropPreferDirect = true
                                end
                                gotoTarget = targetPlayer
                                gotoTargetUserId = targetPlayer.UserId
                            end
                        end
                    end
                end
                if toDeliveryActive and (not dropBaseCFrame) and lastToDropCFrame then
                    dropBaseCFrame = lastToDropCFrame
                end

                if dropBaseCFrame then
                    local myHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                    if myHRP then
                        local releasedForDelivery = false
                        withNoclip(function()
                            local carriedPlayer = carriedCharacter and Players:GetPlayerFromCharacter(carriedCharacter)
                            if (not fastBringCommand) and (not ownerBringStrictMode) and (not dropPreferDirect) then
                                local skyCFrame = getSkyDropCFrame(dropBaseCFrame, carriedPlayer)
                                if skyCFrame then
                                    resetPartVelocity(myHRP)
                                    myHRP.CFrame = skyCFrame
                                    task.wait(0.12)
                                end
                            end

                            local carriedHum = carriedCharacter and carriedCharacter:FindFirstChildOfClass("Humanoid")
                            local carriedHRP = carriedCharacter and carriedCharacter:FindFirstChild("HumanoidRootPart")
                            local myChar = LocalPlayer.Character
                            if ownerBringStrictMode then
                                ownerBringDropValidated = deliverCarriedTargetToOwnerDirectly(
                                    myChar,
                                    myHRP,
                                    carriedCharacter,
                                    gotoTarget,
                                    confirmBringGrab,
                                    true
                                )
                                releasedForDelivery = ownerBringDropValidated
                                if not ownerBringDropValidated then
                                    logDrop("owner direct handoff did not stabilize on owner")
                                end
                                return
                            end
                            local directPos = dropDirectPosition
                            local settleDropCFrame = nil
                            local ownerBringSettleCFrame = nil
                            local function buildFastBringDropState(destinationPos)
                                if not destinationPos then
                                    settleDropCFrame = nil
                                    return nil, nil
                                end

                                if fastBringCommand then
                                    local releasePos = destinationPos
                                    settleDropCFrame = CFrame.new(releasePos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0))
                                    local hoverDropCFrame = CFrame.new(releasePos + Vector3.new(0, FAST_BRING_HOVER_HEIGHT, 0))
                                    return hoverDropCFrame, releasePos
                                end

                                local releaseCFrame = nil
                                if dropPreferDirect and gotoTarget then
                                    releaseCFrame = getIndoorDropCFrame(gotoTarget, carriedCharacter)
                                end
                                if not releaseCFrame then
                                    releaseCFrame = getDropCFrame(CFrame.new(destinationPos), carriedCharacter)
                                end
                                if not releaseCFrame then
                                    releaseCFrame = CFrame.new(destinationPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0))
                                end

                                local releasePos = releaseCFrame.Position
                                settleDropCFrame = CFrame.new(releasePos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0))
                                local hoverDropCFrame = CFrame.new(releasePos + Vector3.new(0, FAST_BRING_HOVER_HEIGHT, 0))
                                return hoverDropCFrame, releasePos
                            end
                            local function refreshLiveDropState(currentDropCFrame, currentReleaseTargetPos)
                                local liveBaseCFrame, liveDirectPos = getPlayerDestinationCFrame(gotoTarget)
                                if liveBaseCFrame then
                                    dropBaseCFrame = liveBaseCFrame
                                    directPos = liveDirectPos
                                    if toDeliveryActive then
                                        lastToDropCFrame = dropBaseCFrame
                                    end
                                end

                                local refreshedDropCFrame = currentDropCFrame
                                if fastBringCommand and directPos then
                                    refreshedDropCFrame, currentReleaseTargetPos = buildFastBringDropState(directPos)
                                elseif dropPreferDirect and gotoTarget then
                                    refreshedDropCFrame = getIndoorDropCFrame(gotoTarget, carriedCharacter)
                                    if not refreshedDropCFrame and directPos then
                                        logDrop("player delivery direct drop fallback")
                                        refreshedDropCFrame = CFrame.new(directPos + Vector3.new(0, 1.5, 0))
                                    end
                                elseif dropBaseCFrame then
                                    refreshedDropCFrame = getDropCFrame(dropBaseCFrame, carriedCharacter)
                                end

                                if refreshedDropCFrame then
                                    return refreshedDropCFrame, currentReleaseTargetPos or refreshedDropCFrame.Position
                                end

                                return currentDropCFrame, currentReleaseTargetPos
                            end
                            local function refreshFastBringSettleState(currentStandCFrame, currentReleaseTargetPos)
                                local refreshedDropCFrame, refreshedReleaseTargetPos = refreshLiveDropState(currentStandCFrame or settleDropCFrame, currentReleaseTargetPos)
                                local refreshedStandCFrame = settleDropCFrame or currentStandCFrame or refreshedDropCFrame
                                if not refreshedStandCFrame and refreshedDropCFrame then
                                    refreshedStandCFrame = refreshedDropCFrame
                                end
                                return refreshedStandCFrame, refreshedReleaseTargetPos or currentReleaseTargetPos
                            end
                            local function refreshOwnerBringSettleState(_, currentReleaseTargetPos)
                                local liveBaseCFrame, liveDirectPos = getPlayerDestinationCFrame(gotoTarget)
                                if liveBaseCFrame then
                                    dropBaseCFrame = liveBaseCFrame
                                    directPos = liveDirectPos
                                end
                                local liveReleasePos = liveDirectPos or currentReleaseTargetPos
                                if not liveReleasePos then
                                    return ownerBringSettleCFrame, currentReleaseTargetPos
                                end
                                ownerBringSettleCFrame = CFrame.new(liveReleasePos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0))
                                return ownerBringSettleCFrame, liveReleasePos
                            end

                            local dropCFrame, releaseTargetPos = refreshLiveDropState(nil, nil)
                            if (not dropCFrame) and fastBringCommand and directPos then
                                dropCFrame, releaseTargetPos = buildFastBringDropState(directPos)
                            end
                            if (not dropCFrame) and dropPreferDirect and gotoTarget then
                                dropCFrame = getIndoorDropCFrame(gotoTarget, carriedCharacter)
                                if not dropCFrame and directPos then
                                    logDrop("player delivery direct drop fallback")
                                    dropCFrame = CFrame.new(directPos + Vector3.new(0, 1.5, 0))
                                end
                            elseif not dropCFrame then
                                dropCFrame = getDropCFrame(dropBaseCFrame, carriedCharacter)
                            end
                            if dropCFrame then
                                releaseTargetPos = releaseTargetPos or dropCFrame.Position
                                if ownerBringStrictMode and releaseTargetPos then
                                    ownerBringSettleCFrame = CFrame.new(releaseTargetPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0))
                                end
                                local targetY = fastBringCommand and releaseTargetPos.Y or dropCFrame.Position.Y
                                resetPartVelocity(myHRP)
                                if carriedHum then
                                    pcall(function()
                                        carriedHum:ChangeState(Enum.HumanoidStateType.Physics)
                                    end)
                                    carriedHum.PlatformStand = true
                                end
                                if carriedHRP then
                                    resetPartVelocity(carriedHRP)
                                end
                                if myChar then
                                    myChar:PivotTo(dropCFrame)
                                else
                                    myHRP.CFrame = dropCFrame
                                end
                                -- CRITICAL: Reset all velocities immediately after move to prevent bounce/upswing
                                resetPartVelocity(myHRP)
                                if carriedHRP then
                                    resetPartVelocity(carriedHRP)
                                end
                                local standDistance = strictDropMode and STRICT_DROP_STAND_DISTANCE or (fastBringCommand and FAST_BRING_STAND_DISTANCE or 12)
                                local carriedDistance = strictDropMode and STRICT_DROP_CARRIED_DISTANCE or (fastBringCommand and FAST_BRING_CARRIED_DISTANCE or 16)
                                local standArrived, carriedArrived = alignCarryDropPosition(
                                    myChar,
                                    myHRP,
                                    carriedHRP,
                                    dropCFrame,
                                    releaseTargetPos,
                                    (fastBringCommand or ownerBringStrictMode) and FAST_BRING_SYNC_TIMEOUT or DROP_SYNC_TIMEOUT,
                                    standDistance,
                                    carriedDistance,
                                    gotoTarget and refreshLiveDropState or nil,
                                    strictDropMode
                                )
                                if not standArrived then
                                    logDrop("stand did not reach drop destination before release")
                                end
                                if carriedHRP and not carriedArrived then
                                    logDrop("carried target desync before release")
                                end
                                -- Clamp the carried target so they never exceed the intended drop height.
                                clampOwnerAboveTarget(myChar, myHRP, carriedHRP, targetY)
                                -- Additional velocity reset after clamp to prevent any residual motion
                                if carriedHRP then
                                    resetPartVelocity(carriedHRP)
                                end
                                task.wait(fastBringCommand and 0.03 or 0.06)
                                if gotoTarget then
                                    local refreshedDropCFrame, refreshedReleaseTargetPos = refreshLiveDropState(dropCFrame, releaseTargetPos)
                                    if refreshedDropCFrame then
                                        dropCFrame = refreshedDropCFrame
                                        releaseTargetPos = refreshedReleaseTargetPos or dropCFrame.Position
                                        targetY = fastBringCommand and releaseTargetPos.Y or dropCFrame.Position.Y
                                        moveStandToCFrameExact(myChar, myHRP, dropCFrame)
                                        if carriedHRP then
                                            resetPartVelocity(carriedHRP)
                                        end
                                        standArrived = isNearPosition(myHRP, releaseTargetPos, standDistance)
                                        if carriedHRP then
                                            carriedArrived = isNearPosition(carriedHRP, releaseTargetPos, carriedDistance)
                                        end
                                    end
                                end
                                local canRelease = true
                                if strictDropMode and not confirmBringGrab() then
                                    canRelease = false
                                    logDrop("lost delivery grab before release; retrying")
                                end
                                if canRelease and ownerBringStrictMode and ownerBringSettleCFrame then
                                    local pinStandArrived, pinCarriedArrived, pinnedStandCFrame, pinnedReleaseTargetPos = pinCarryDropPosition(
                                        myChar,
                                        myHRP,
                                        carriedHRP,
                                        ownerBringSettleCFrame,
                                        releaseTargetPos,
                                        FAST_BRING_PIN_LOOPS,
                                        FAST_BRING_PIN_WAIT,
                                        FAST_BRING_FINAL_STAND_DISTANCE,
                                        FAST_BRING_FINAL_CARRIED_DISTANCE,
                                        confirmBringGrab,
                                        gotoTarget and refreshOwnerBringSettleState or nil,
                                        true
                                    )
                                    if pinnedStandCFrame then
                                        ownerBringSettleCFrame = pinnedStandCFrame
                                    end
                                    if pinnedReleaseTargetPos then
                                        releaseTargetPos = pinnedReleaseTargetPos
                                    end
                                    standArrived = pinStandArrived
                                    if carriedHRP then
                                        carriedArrived = pinCarriedArrived
                                    end
                                end
                                if canRelease and fastBringCommand and settleDropCFrame then
                                    local pinStandArrived, pinCarriedArrived, pinnedStandCFrame, pinnedReleaseTargetPos = pinCarryDropPosition(
                                        myChar,
                                        myHRP,
                                        carriedHRP,
                                        settleDropCFrame,
                                        releaseTargetPos,
                                        FAST_BRING_PIN_LOOPS,
                                        FAST_BRING_PIN_WAIT,
                                        FAST_BRING_FINAL_STAND_DISTANCE,
                                        FAST_BRING_FINAL_CARRIED_DISTANCE,
                                        confirmBringGrab,
                                        gotoTarget and refreshFastBringSettleState or nil,
                                        false
                                    )
                                    if pinnedStandCFrame then
                                        settleDropCFrame = pinnedStandCFrame
                                    end
                                    if pinnedReleaseTargetPos then
                                        releaseTargetPos = pinnedReleaseTargetPos
                                    end
                                    standArrived = pinStandArrived
                                    if carriedHRP then
                                        carriedArrived = pinCarriedArrived
                                    end
                                end
                                if canRelease and not standArrived then
                                    canRelease = false
                                    logDrop("stand not at delivery destination yet; retrying")
                                end
                                if canRelease and carriedHRP and not carriedArrived then
                                    canRelease = false
                                    logDrop("carried target not synced at destination yet; retrying")
                                end
                                if canRelease and ownerBringStrictMode and ownerBringSettleCFrame then
                                    moveStandToCFrameExact(myChar, myHRP, ownerBringSettleCFrame)
                                    resetPartVelocity(myHRP)
                                    if carriedHRP then
                                        resetPartVelocity(carriedHRP)
                                    end
                                end
                                if canRelease and fastBringCommand and settleDropCFrame then
                                    moveStandToCFrameExact(myChar, myHRP, settleDropCFrame)
                                    resetPartVelocity(myHRP)
                                    if carriedHRP then
                                        resetPartVelocity(carriedHRP)
                                    end
                                end
                                if canRelease and strictDeliveryGrab then
                                    local strictReady = isStrictDeliveryReadyForReleaseStable(
                                        myHRP,
                                        carriedHRP,
                                        carriedCharacter,
                                        STRICT_DROP_RELEASE_STAND_DISTANCE,
                                        STRICT_DROP_RELEASE_CARRIED_DISTANCE,
                                        STRICT_DROP_RELEASE_CONFIRM_LOOPS,
                                        STRICT_DROP_RELEASE_CONFIRM_WAIT
                                    )
                                    if not strictReady then
                                        canRelease = false
                                        logDrop("strict .to release blocked until stand and carried target are both at destination")
                                    end
                                end
                                if canRelease then
                                    releasedForDelivery = releaseGrabReliably(
                                        confirmBringGrab,
                                        fastBringCommand and FAST_BRING_RELEASE_ATTEMPTS or DROP_RELEASE_ATTEMPTS,
                                        fastBringCommand and FAST_BRING_RELEASE_WAIT or DROP_RELEASE_WAIT,
                                        {
                                            lockout = strictDeliveryGrab and BRING_GRAB_LOCKOUT_TIME or nil,
                                        }
                                    )
                                    if not releasedForDelivery then
                                        logDrop("release confirmation failed; retrying")
                                    elseif strictDropMode and not fastBringCommand and not ownerBringStrictMode and settleDropCFrame and carriedHRP then
                                        local postReleaseStandArrived, postReleaseCarriedArrived, pinnedStandCFrame, pinnedReleaseTargetPos = pinCarryDropPosition(
                                            myChar,
                                            myHRP,
                                            carriedHRP,
                                            settleDropCFrame,
                                            releaseTargetPos,
                                            STRICT_DROP_POST_RELEASE_PIN_LOOPS,
                                            STRICT_DROP_POST_RELEASE_PIN_WAIT,
                                            STRICT_DROP_STAND_DISTANCE,
                                            STRICT_DROP_CARRIED_DISTANCE,
                                            nil,
                                            gotoTarget and refreshLiveDropState or nil,
                                            true
                                        )
                                        if pinnedStandCFrame then
                                            settleDropCFrame = pinnedStandCFrame
                                        end
                                        if pinnedReleaseTargetPos then
                                            releaseTargetPos = pinnedReleaseTargetPos
                                        end
                                        strictDeliveryDropValidated = postReleaseStandArrived and postReleaseCarriedArrived
                                        if not strictDeliveryDropValidated then
                                            logDrop("strict delivery post-release handoff did not fully settle on destination")
                                        end
                                    elseif fastBringCommand and settleDropCFrame and carriedHRP then
                                        local postReleaseStandArrived, postReleaseCarriedArrived, pinnedStandCFrame, pinnedReleaseTargetPos = pinCarryDropPosition(
                                            myChar,
                                            myHRP,
                                            carriedHRP,
                                            settleDropCFrame,
                                            releaseTargetPos,
                                            FAST_BRING_POST_RELEASE_PIN_LOOPS,
                                            FAST_BRING_POST_RELEASE_PIN_WAIT,
                                            FAST_BRING_FINAL_STAND_DISTANCE,
                                            FAST_BRING_FINAL_CARRIED_DISTANCE,
                                            nil,
                                            gotoTarget and refreshFastBringSettleState or nil,
                                            false
                                        )
                                        if pinnedStandCFrame then
                                            settleDropCFrame = pinnedStandCFrame
                                        end
                                        if pinnedReleaseTargetPos then
                                            releaseTargetPos = pinnedReleaseTargetPos
                                        end
                                        if not postReleaseStandArrived or not postReleaseCarriedArrived then
                                            logDrop("fast bring post-release handoff did not fully settle on owner")
                                        end
                                    end
                                end
                                if releasedForDelivery and ownerBringStrictMode then
                                    local ownerStable, liveOwnerPos = stabilizeReleasedCarryAtPlayer(
                                        myChar,
                                        myHRP,
                                        carriedHRP,
                                        gotoTarget,
                                        OWNER_BRING_POST_RELEASE_PIN_LOOPS,
                                        OWNER_BRING_POST_RELEASE_PIN_WAIT,
                                        OWNER_BRING_POST_RELEASE_REQUIRED_HITS,
                                        OWNER_BRING_FINAL_TARGET_DISTANCE,
                                        FAST_BRING_SETTLE_HEIGHT,
                                        true
                                    )
                                    if ownerStable then
                                        ownerBringDropValidated = true
                                    else
                                        logDrop("owner bring release did not keep target on owner")
                                        if liveOwnerPos and carriedHRP then
                                            logDrop(("owner bring target ended at %.2f, %.2f, %.2f instead of owner %.2f, %.2f, %.2f"):format(
                                                carriedHRP.Position.X,
                                                carriedHRP.Position.Y,
                                                carriedHRP.Position.Z,
                                                liveOwnerPos.X,
                                                liveOwnerPos.Y,
                                                liveOwnerPos.Z
                                            ))
                                        end
                                    end
                                end
                                if releasedForDelivery and fastBringCommand then
                                    local _, liveOwnerPos = getPlayerDestinationCFrame(gotoTarget)
                                    if carriedHRP and liveOwnerPos and isNearPosition(carriedHRP, liveOwnerPos, FAST_BRING_FINAL_CARRIED_DISTANCE + 2) then
                                        fastBringDropValidated = true
                                    else
                                        logDrop("fast bring release was not at owner position")
                                    end
                                end
                                task.wait(fastBringCommand and 0.05 or 0.06)
                                local exitCFrame = nil
                                if fastBringCommand or ownerBringStrictMode then
                                    local exitBasePos = releaseTargetPos
                                    if gotoTarget then
                                        local _, liveExitPos = getPlayerDestinationCFrame(gotoTarget)
                                        exitBasePos = liveExitPos or exitBasePos
                                    end
                                    if exitBasePos then
                                        exitCFrame = getNorthSouthCarryCFrame(
                                            exitBasePos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, DROP_BACK_OFFSET.Z * 0.75)
                                        )
                                    end
                                else
                                    exitCFrame = getDropExitCFrame(dropBaseCFrame)
                                end
                                if exitCFrame then
                                    if myChar then
                                        myChar:PivotTo(exitCFrame)
                                    else
                                        myHRP.CFrame = exitCFrame
                                    end
                                end
                                if carriedHRP then
                                    resetPartVelocity(carriedHRP)
                                end
                                if carriedHum then
                                    carriedHum.PlatformStand = false
                                    pcall(function()
                                        carriedHum:ChangeState(Enum.HumanoidStateType.GettingUp)
                                    end)
                                end
                            end
                        end)

                        if releasedForDelivery then
                            local passiveReleaseConfirmed = false
                            for _ = 1, 3 do
                                task.wait(0.06)
                                local releaseLinkCleared = isCarryReleaseConfirmed(carriedCharacter)
                                local releaseGrabCleared = not confirmBringGrab()
                                if releaseLinkCleared and releaseGrabCleared then
                                    passiveReleaseConfirmed = true
                                    break
                                end
                            end

                            if ownerBringStrictMode or fastBringCommand then
                                local exitBasePos = nil
                                if gotoTarget then
                                    local _, liveExitPos = getPlayerDestinationCFrame(gotoTarget)
                                    exitBasePos = liveExitPos
                                end
                                if (not exitBasePos) and releaseTargetPos then
                                    exitBasePos = releaseTargetPos
                                end
                                if exitBasePos then
                                    local ownerExitCFrame = getNorthSouthCarryCFrame(
                                        exitBasePos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, DROP_BACK_OFFSET.Z * 0.75)
                                    )
                                    moveStandToCFrameExact(myChar, myHRP, ownerExitCFrame)
                                    resetPartVelocity(myHRP)
                                end
                            end

                            if ownerBringStrictMode then
                                didDrop = ownerBringDropValidated and (passiveReleaseConfirmed or isCarryReleaseConfirmed(carriedCharacter))
                            elseif strictDropMode and not fastBringCommand then
                                didDrop = strictDeliveryDropValidated and (passiveReleaseConfirmed or isCarryReleaseConfirmed(carriedCharacter))
                            else
                                didDrop = ((not fastBringCommand) or fastBringDropValidated) and (passiveReleaseConfirmed or isCarryReleaseConfirmed(carriedCharacter))
                            end
                        elseif not strictDropMode then
                            didDrop = releasedForDelivery
                        end
                    end
                end

                if not didDrop then
                    if toDeliveryActive and not dropBaseCFrame then
                        logDrop("delivery destination unresolved; retrying without release")
                    elseif fastBringCommand or ownerBringStrictMode then
                        logDrop("owner handoff not synced yet; holding target and retrying")
                    else
                        -- Fallback: original simple delivery
                        local fallbackMoved = false
                        local fallbackDropPos = nil
                        local carriedFallbackHRP = carriedCharacter and carriedCharacter:FindFirstChild("HumanoidRootPart")
                        if gotoCFrame then
                            local myHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                            if myHRP then
                                fallbackDropPos = gotoCFrame.Position
                                for _ = 1, DROP_MOVE_ATTEMPTS do
                                    myHRP.CFrame = gotoCFrame
                                    resetPartVelocity(myHRP)
                                    task.wait(0.05)
                                    if isNearPosition(myHRP, fallbackDropPos, 16) then
                                        fallbackMoved = true
                                        break
                                    end
                                end
                            end
                        elseif gotoTarget and gotoTarget.Character then
                            local myHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                            if myHRP then
                                for _ = 1, DROP_MOVE_ATTEMPTS do
                                    local _, liveDropPos = getPlayerDestinationCFrame(gotoTarget)
                                    if not liveDropPos then
                                        break
                                    end
                                    fallbackDropPos = liveDropPos
                                    local fallbackCFrame = CFrame.new(liveDropPos + Vector3.new(0, 3, 0))
                                    myHRP.CFrame = fallbackCFrame
                                    resetPartVelocity(myHRP)
                                    task.wait(0.05)
                                    if isNearPosition(myHRP, fallbackDropPos, 16) then
                                        fallbackMoved = true
                                        break
                                    end
                                end
                            end
                        else
                            if strictDropMode then
                                logDrop("delivery fallback missing destination; retrying without release")
                            else
                                local dropRecipient = commandSender and Players:FindFirstChild(commandSender)
                                local myHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                                if myHRP and dropRecipient then
                                    for _ = 1, DROP_MOVE_ATTEMPTS do
                                        local _, liveDropPos = getPlayerDestinationCFrame(dropRecipient)
                                        if not liveDropPos then
                                            break
                                        end
                                        fallbackDropPos = liveDropPos
                                        local fallbackCFrame = CFrame.new(liveDropPos + Vector3.new(0, 3, 0))
                                        myHRP.CFrame = fallbackCFrame
                                        resetPartVelocity(myHRP)
                                        task.wait(0.05)
                                        if isNearPosition(myHRP, fallbackDropPos, 14) then
                                            fallbackMoved = true
                                            break
                                        end
                                    end
                                else
                                    teleportToTarget(commandSender)
                                    task.wait(0.2)
                                    fallbackMoved = true
                                end
                            end
                        end
                        local canFallbackRelease = true
                        if strictDropMode and not fallbackMoved then
                            canFallbackRelease = false
                            logDrop("fallback not at destination yet; retrying without release")
                        end
                        if canFallbackRelease and gotoTarget then
                            local _, liveDropPos = getPlayerDestinationCFrame(gotoTarget)
                            if liveDropPos then
                                fallbackDropPos = liveDropPos
                            end
                        elseif canFallbackRelease and commandSender then
                            local dropRecipient = Players:FindFirstChild(commandSender)
                            local _, liveDropPos = getPlayerDestinationCFrame(dropRecipient)
                            if liveDropPos then
                                fallbackDropPos = liveDropPos
                            end
                        end
                        local fallbackStandHRP = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                        if canFallbackRelease and fallbackDropPos and fallbackStandHRP and not isNearPosition(fallbackStandHRP, fallbackDropPos, 14) then
                            canFallbackRelease = false
                            logDrop("fallback stand position is not at destination yet; retrying")
                        end
                        if canFallbackRelease and fallbackDropPos and carriedFallbackHRP and not isNearPosition(carriedFallbackHRP, fallbackDropPos, 16) then
                            canFallbackRelease = false
                            logDrop("fallback carried target position is not at destination yet; retrying")
                        end
                        if canFallbackRelease and strictDeliveryGrab then
                            local strictReady = isStrictDeliveryReadyForReleaseStable(
                                fallbackStandHRP,
                                carriedFallbackHRP,
                                carriedCharacter,
                                STRICT_DROP_RELEASE_STAND_DISTANCE,
                                STRICT_DROP_RELEASE_CARRIED_DISTANCE,
                                STRICT_DROP_RELEASE_CONFIRM_LOOPS,
                                STRICT_DROP_RELEASE_CONFIRM_WAIT
                            )
                            if not strictReady then
                                canFallbackRelease = false
                                logDrop("strict .to fallback release blocked until delivery is fully synced")
                            end
                        end
                        if canFallbackRelease then
                            didDrop = releaseGrabReliably(
                                confirmBringGrab,
                                DROP_RELEASE_ATTEMPTS,
                                DROP_RELEASE_WAIT,
                                {
                                    lockout = strictDeliveryGrab and BRING_GRAB_LOCKOUT_TIME or nil,
                                }
                            )
                        end
                    end
                end
                local stillHoldingAfterDrop = confirmBringGrab()
                local releaseValidatedWithoutGrab = false
                if not stillHoldingAfterDrop then
                    if ownerBringStrictMode then
                        releaseValidatedWithoutGrab = ownerBringDropValidated
                    elseif fastBringCommand then
                        releaseValidatedWithoutGrab = fastBringDropValidated
                    elseif strictDropMode then
                        releaseValidatedWithoutGrab = strictDeliveryDropValidated
                    else
                        releaseValidatedWithoutGrab = true
                    end
                end
                if strictDeliveryGrab and not releaseValidatedWithoutGrab then
                    local carriedFinalPart = character:FindFirstChild("HumanoidRootPart")
                        or character:FindFirstChild("UpperTorso")
                        or character:FindFirstChild("Torso")
                    local finalStandChar = LocalPlayer.Character
                    local standFinalHRP = finalStandChar and finalStandChar:FindFirstChild("HumanoidRootPart")
                    local deliveryBaseCFrame = gotoCFrame or lastToDropCFrame
                    local deliveryPos = deliveryBaseCFrame and deliveryBaseCFrame.Position or nil
                    if gotoTarget then
                        local _, liveDeliveryPos = getPlayerDestinationCFrame(gotoTarget)
                        deliveryPos = liveDeliveryPos or deliveryPos
                    end
                    if deliveryPos and carriedFinalPart and standFinalHRP then
                        local carriedAtDestination = isNearPosition(
                            carriedFinalPart,
                            deliveryPos,
                            STRICT_DROP_RELEASE_CARRIED_DISTANCE + 1
                        )
                        local standAtDestination = isNearPosition(
                            standFinalHRP,
                            deliveryPos,
                            STRICT_DROP_RELEASE_STAND_DISTANCE + 0.75
                        )
                        if carriedAtDestination and standAtDestination then
                            local settleCFrame = getNorthSouthGrabCFrame(
                                deliveryPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, 0)
                            )
                            moveStandToCFrameExact(finalStandChar, standFinalHRP, settleCFrame)
                            resetPartVelocity(standFinalHRP)
                            resetPartVelocity(carriedFinalPart)
                            task.wait(0.04)

                            local forcedRelease = releaseGrabReliably(
                                confirmBringGrab,
                                DROP_RELEASE_ATTEMPTS + 6,
                                DROP_RELEASE_WAIT,
                                {
                                    lockout = BRING_GRAB_LOCKOUT_TIME,
                                    releaseCheck = function()
                                        return isCarryReleaseConfirmed(character)
                                    end,
                                }
                            )

                            if not forcedRelease then
                                local exitCFrame = getNorthSouthCarryCFrame(
                                    deliveryPos + Vector3.new(0, FAST_BRING_SETTLE_HEIGHT, DROP_BACK_OFFSET.Z * 0.55)
                                )
                                moveStandToCFrameExact(finalStandChar, standFinalHRP, exitCFrame)
                                resetPartVelocity(standFinalHRP)
                                resetPartVelocity(carriedFinalPart)
                                task.wait(0.05)

                                forcedRelease = releaseGrabReliably(
                                    confirmBringGrab,
                                    DROP_RELEASE_ATTEMPTS + 6,
                                    DROP_RELEASE_WAIT,
                                    {
                                        lockout = BRING_GRAB_LOCKOUT_TIME,
                                        releaseCheck = function()
                                            return isCarryReleaseConfirmed(character)
                                        end,
                                    }
                                )
                            end

                            if forcedRelease and isNearPosition(carriedFinalPart, deliveryPos, STRICT_DROP_RELEASE_CARRIED_DISTANCE + 1.5) then
                                releaseValidatedWithoutGrab = true
                                stillHoldingAfterDrop = false
                                strictDeliveryDropValidated = true
                                logDrop("strict delivery release confirmed at destination")
                            else
                                logDrop("strict delivery reached destination but grab is still active; retrying")
                            end
                        end
                    end
                end
                local releaseCompleted = didDrop or releaseValidatedWithoutGrab
                if releaseCompleted then
                    clearStandCommandBusy()
                    local completedDelivery = releaseCompleted and toDeliveryActive
                    local fastBringDelivered = didDrop and fastBringCommand
                    local ownerBringDelivered = didDrop and ownerBringStrictMode
                    local delayVoid = (completedDelivery or fastBringDelivered or ownerBringDelivered) and (dropPreferDirect or gotoTarget or gotoTargetUserId or fastBringDelivered or ownerBringDelivered)

                    -- Always clear the live carry state first.
                    -- If there is a saved task to resume, restoreDeliveryResumeState() will reapply it.
                    lockedTarget = nil
                    lockedTargetUserId = nil
                    autoLocked = false
                    bringonly = false
                    teleporting = false

                    -- Clear delivery destination before optional task resume.
                    gotoCFrame = nil
                    gotoTarget = nil
                    gotoTargetUserId = nil
                    pendingGotoTarget = nil
                    pendingGotoTargetUserId = nil
                    forceBringDrop = false
                    lastToDestination = nil
                    toDeliveryActive = false
                    lastToDropCFrame = nil
                    commandSender = nil
                    skyTarget = nil
                    savedTarget5 = nil

                    local resumedTask = false
                    if completedDelivery then
                        resumedTask = restoreDeliveryResumeState()
                    else
                        clearDeliveryResumeState()
                    end

                    task.delay(0.08, function()
                        if not bringonly and not takeonly and not toDeliveryActive then
                            pcall(function()
                                ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                            end)
                        end
                    end)

                    if not resumedTask then
                        local releasedPlayer = carriedCharacter and Players:GetPlayerFromCharacter(carriedCharacter)
                        local immediatePostDropTransition = completedDelivery or fastBringDelivered or ownerBringDelivered
                        recentBringReleasedUserId = releasedPlayer and releasedPlayer.UserId or nil
                        recentBringReleaseUntil = os.clock() + (immediatePostDropTransition and 0.18 or (delayVoid and 1.15 or 0.8))
                        voiding = false

                        if immediatePostDropTransition then
                            if not (autosaveActive or bringonly or takeonly or toDeliveryActive or isCurrentlyGrabbing()) then
                                if not resumeOwnerFollow() and not isCurrentlyGrabbing() then
                                    voiding = true
                                else
                                    voiding = false
                                end
                            end
                        else
                            task.delay(delayVoid and 0.55 or 0.18, function()
                                if autosaveActive or bringonly or takeonly or toDeliveryActive or isCurrentlyGrabbing() then
                                    return
                                end
                                if os.clock() < (recentBringReleaseUntil or 0) then
                                    return
                                end
                                resumeOwnerFollow()
                                voiding = false
                            end)
                        end
                    end
                    resetBringGrabAttemptState()
                    requestPostCarryCombatRecovery(lockedTarget or sentrytarget, true)
                    reloadTool()
                else
                    if not toDeliveryActive then
                        local carriedPlayer = carriedCharacter and Players:GetPlayerFromCharacter(carriedCharacter)
                        if carriedPlayer and carriedPlayer.Character == carriedCharacter then
                            lockedTarget = carriedPlayer
                            lockedTargetUserId = carriedPlayer.UserId
                        end
                    end
                    teleporting = not stillHoldingAfterDrop
                    voiding = false
                end
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

takeconnection = nil

task.spawn(function()
    while true do
        if hardStop then
            task.wait(standWait(perf.combat))
            continue
        end
        if takeonly and lockedTarget and lockedTarget.Character and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            local character = lockedTarget.Character

            local bodyEffects = character and character:FindFirstChild("BodyEffects")

            local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
            local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value

            local grabbed = false

            local character = lockedTarget.Character
            local humanoidRootPart = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            local upperTorso = character and character:FindFirstChild("UpperTorso")

            if takeconnection then
                takeconnection:Disconnect()
                takeconnection = nil
            end

            takeconnection = character.ChildAdded:Connect(function(child)
                if child.Name == "GRABBING_CONSTRAINT" then
                    grabbed = true
                    lockedTarget = nil
                    if takeconnection then takeconnection:Disconnect() takeconnection = nil end
                end
            end)

            if character:FindFirstChild("GRABBING_CONSTRAINT") then
                grabbed = true
                lockedTarget = nil
                if takeconnection then takeconnection:Disconnect() takeconnection = nil end
            end

            if not grabbed and isKO and humanoidRootPart and upperTorso then
                teleporting = false
                voiding = false

                humanoidRootPart.Velocity = Vector3.zero
                humanoidRootPart.RotVelocity = Vector3.zero
                humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
                humanoidRootPart.AssemblyAngularVelocity = Vector3.zero
                humanoidRootPart.CFrame = CFrame.new(upperTorso.Position + Vector3.new(0, 3.5, 0))
                if not autosaveActive then
                    ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                end
                task.wait(0.3)
            else
                teleporting = true
                voiding = false
            end

            if grabbed then
                local localChar = LocalPlayer.Character
                local hrp = localChar and localChar:FindFirstChild("HumanoidRootPart")

                if skyTarget and hrp then
                    lockedTarget = nil
                    hrp.CFrame = CFrame.new(0, -999999999, 0)
                    task.wait(0.3)
                    if not autosaveActive then
                        ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                    end
                    task.wait(0.3)
                    voiding = true
                    reloadTool()
                    skyTarget = nil
                end

                if gotoCFrame and gotoPlayer and hrp then
                    lockedTarget = nil
                    hrp.CFrame = gotoCFrame
                    task.wait(0.3)
                    if not autosaveActive then
                        ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                    end
                    task.wait(0.3)
                    voiding = true
                    reloadTool()
                    gotoPlayer = nil
                    gotoCFrame = nil
                    gotoTarget = nil
                    vehicleModel = nil
                end

                if savedTarget5 then
                    local dstChar = savedTarget5.Character
                    if dstChar and dstChar:FindFirstChild("HumanoidRootPart") and hrp then
                        lockedTarget = nil
                        local dstPos = dstChar.HumanoidRootPart.Position
                        teleportToPosition(dstPos)
                        task.wait(0.3)
                        if not autosaveActive then
                            ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                        end
                        task.wait(0.3)
                        voiding = true
                        reloadTool()
                    end
                    savedTarget5 = nil
                end
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

task.spawn(function()
    while true do
        if getgenv().downonly and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) and not stomponly and not bringonly and not takeonly and not opkill and lockedTarget then
            local character = lockedTarget.Character
            if character then
                local bodyEffects = character:FindFirstChild("BodyEffects")
                local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value

                if not isKO and not isSDeath then
                    teleporting = true
                    voiding = false
                elseif isKO or isSDeath then
                    -- For loopknock (.lk) we want to keep re-targeting the same player after they respawn.
                    -- Clearing lockedTarget here stops the loop after the first KO.
                    if #ragebottargets > 0 then
                        shouldSwitch = true
                    end
                    teleporting = false
                    voiding = true
                    reloadTool()
                end
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

Players = game:GetService("Players")
LocalPlayer = Players.LocalPlayer

task.spawn(function()
    while true do
        if opkill and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) and not stomponly and not bringonly and not takeonly and not getgenv().downonly and lockedTarget then
            local character = lockedTarget.Character
            if character then
                local bodyEffects = character:FindFirstChild("BodyEffects")
                local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
                local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
                local isGrabbed = character:FindFirstChild("GRABBING_CONSTRAINT")
                local hasForceField = character:FindFirstChildOfClass("ForceField")

                if not isKO and not isSDeath and not isGrabbed and not hasForceField then
                    teleporting = true
                    voiding = false
                elseif isKO or isSDeath or isGrabbed or hasForceField then
                    voiding = true
                    teleporting = false
                end
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

task.spawn(function()
    while true do
        if flingonly and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) and not stomponly and not bringonly and not takeonly and not getgenv().downonly and lockedTarget then
            local char = Player.Character
            local targetHRP = lockedTarget.Character and lockedTarget.Character:FindFirstChild("HumanoidRootPart")

            if char and char:FindFirstChild("HumanoidRootPart") and targetHRP then
                teleporting = true
                voiding = false
                local offset
                if smiteCommandInProgress then
                    offset = Vector3.new(math.random(-2, 2), math.random(-1, 1), math.random(-2, 2))
                else
                    offset = Vector3.new(0, 0, math.random(-30, 30))
                end

                char.HumanoidRootPart.CFrame = CFrame.new(
                    targetHRP.Position + offset
                )
            end
        end
        task.wait(standWait(perf.combat))
    end
end)

task.spawn(function()
    while true do
        if hardStop then
            task.wait(standWait(perf.killall))
            continue
        end
        if killall and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then

            local switchTarget = false
            if lockedTarget and lockedTarget.Character then
                local character = lockedTarget.Character
                local bodyEffects = character:FindFirstChild("BodyEffects")
                local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
                if isSDeath then
                    switchTarget = true
                end
            else
                switchTarget = true
            end

            if switchTarget then
                local candidates = {}
                for _, player in pairs(Players:GetPlayers()) do
                    if player.Name ~= Owner
                       and player ~= Players.LocalPlayer
                       and player.Character 
                       and player.Character:FindFirstChild("BodyEffects") 
                       and player.Character.BodyEffects:FindFirstChild("SDeath") 
                       and not player.Character.BodyEffects["SDeath"].Value
                       and not player.Character:FindFirstChild("GRABBING_CONSTRAINT") then
                        table.insert(candidates, player)
                    end
                end

                if #candidates > 0 then
                    lockedTarget = candidates[math.random(1, #candidates)]
                end
            end
        end
        task.wait(standWait(perf.killall))
    end
end)

RunService.Heartbeat:Connect(function()
    if hardStop then
        return
    end
    if postResetCombatRecoveryActive or buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress then
        return
    end
    local targetCharacter
    local target

    if lockedTarget and lockedTarget.Character then
        targetCharacter = lockedTarget.Character
        target = lockedTarget
    elseif sentrytarget and sentrytarget.Character then
        targetCharacter = sentrytarget.Character
        target = sentrytarget
    end

    if not targetCharacter or not targetCharacter:FindFirstChild("HumanoidRootPart") then return end
    if target == LocalPlayer then
        lockedTarget = nil
        voiding = true
        return
    end

    local targetHRP = targetCharacter:FindFirstChild("HumanoidRootPart")
    local targetHead = targetCharacter:FindFirstChild("Head")
    local flameFocusMode = flameModeActive
        and flameModeTargetUserId
        and target == lockedTarget
        and lockedTarget
        and lockedTarget.UserId == flameModeTargetUserId
    local targetPart = (flameFocusMode and targetHead) or targetHead or targetHRP
    local isGrabbed = targetCharacter:FindFirstChild("GRABBING_CONSTRAINT")

    if not targetHRP or not targetPart or not targetPart.Parent then return end
    if isGrabbed then return end
    if (flingonly and target) then return end

    local bodyEffects = targetCharacter:FindFirstChild("BodyEffects")
    local koValue = bodyEffects and bodyEffects:FindFirstChild("K.O")
    local isKO = koValue and koValue.Value
    if isKO and (#ragebottargets > 0) then
        return
    end

    local playerChar = game.Players.LocalPlayer.Character
    if not playerChar then return end

    local playerHRP = playerChar:FindFirstChild("HumanoidRootPart")
    if not playerHRP then return end

    local loopModeActive = (#ragebottargets > 0) and target and lockedTarget and (target == lockedTarget)
    local sentryModeActive = sentrytarget and target and (target == sentrytarget)
    local circleShotMode = target
        and not flameFocusMode
        and not bringonly
        and not takeonly
        and not flingonly
        and ((lockedTarget and target == lockedTarget) or sentryModeActive)
    local directAttackMode = circleShotMode and not loopModeActive and not sentryModeActive
    local effectiveInterval = shootInterval
    local effectiveShots = shotsPerTick
    local loopInstantFire = loopModeActive
    local targetIndoors = getLoopIndoors(target)
    if loopModeActive then
        targetIndoors = targetIndoors or loopIsInBuilding or (os.clock() < loopBlockedSightUntil)
    end
    if targetIndoors then
        effectiveInterval = combatConfig.indoorShootInterval
        effectiveShots = combatConfig.indoorShotsPerTick
    end
    if directAttackMode then
        effectiveInterval = math.min(effectiveInterval, combatConfig.attackShootInterval or effectiveInterval)
        effectiveShots = math.max(effectiveShots, combatConfig.attackShotsPerTick or effectiveShots)
        loopInstantFire = true
    end
    if loopModeActive then
        effectiveInterval = math.min(effectiveInterval, combatConfig.loopShootInterval or effectiveInterval)
        effectiveShots = math.max(effectiveShots, combatConfig.loopShotsPerTick or effectiveShots)
        if targetIndoors then
            effectiveShots = math.max(effectiveShots, (combatConfig.loopShotsPerTick or effectiveShots) + 2)
        end
    elseif sentryModeActive then
        effectiveInterval = math.min(effectiveInterval, combatConfig.sentryShootInterval or effectiveInterval)
        effectiveShots = math.max(effectiveShots, combatConfig.sentryShotsPerTick or effectiveShots)
        loopInstantFire = true
    end
    if flameFocusMode then
        effectiveInterval = FLAME_HOLD_CLICK_INTERVAL
        effectiveShots = 1
        loopInstantFire = false
    end
    if not flameFocusMode then
        effectiveShots = effectiveShots * getNetworkBurstScale(false)
    end
    effectiveShots = clamp(math.floor(effectiveShots + 0.5), 1, standTuning.maxBurstShots or 6)
    local now = os.clock()
    if (combatPrimeWindowUntil or 0) > now then
        requestCombatAttackPrime(target, false)
    end
    if loopInstantFire then
        local instantMinShootInterval
        if loopModeActive then
            instantMinShootInterval = combatConfig.loopMinShootInterval or 0.006
        elseif sentryModeActive then
            instantMinShootInterval = combatConfig.sentryMinShootInterval or combatConfig.loopMinShootInterval or 0.006
        else
            instantMinShootInterval = combatConfig.attackMinShootInterval or combatConfig.loopMinShootInterval or 0.006
        end
        if powerModeActive then
            if loopModeActive then
                instantMinShootInterval = math.max(instantMinShootInterval, 0.0033)
            elseif sentryModeActive then
                instantMinShootInterval = math.max(instantMinShootInterval, 0.0031)
            else
                instantMinShootInterval = math.max(instantMinShootInterval, 0.0028)
            end
        end
        if (now - lastShootAt) < instantMinShootInterval then
            return
        end
    else
        effectiveInterval = math.max(effectiveInterval, standTuning.minShootInterval or 0.02)
        if (now - lastShootAt) < effectiveInterval then
            return
        end
    end
    lastShootAt = now

    local origin = playerHRP.Position
    local distance = (targetPart.Position - origin).Magnitude
    local targetVelocity = targetHRP.AssemblyLinearVelocity or targetHRP.Velocity or Vector3.zero
    local trackedVelocity = (followState.currentTargetCharacter == targetCharacter) and (followState.targetVelocity or Vector3.zero) or Vector3.zero
    if trackedVelocity.Magnitude > targetVelocity.Magnitude then
        targetVelocity = trackedVelocity
    end
    local targetSpeed = targetVelocity.Magnitude
    local fastTargetThreshold = combatConfig.fastTargetSpeedThreshold or 85
    local extremeTargetThreshold = combatConfig.extremeTargetSpeedThreshold or (fastTargetThreshold * 2)
    local fastTarget = targetSpeed >= fastTargetThreshold
    local extremeTarget = targetSpeed >= extremeTargetThreshold
    local standDuelTarget = followState.standDuelTarget
        and not bringonly
        and not takeonly
        and not flingonly
        and (loopModeActive or directAttackMode or sentryModeActive)
    local standDuelExtreme = standDuelTarget and followState.standDuelExtreme

    local allowedRange = combatConfig.maxRange
    local sightMultiplier = combatConfig.sightRangeMultiplier
    local blindRange = nil
    if loopModeActive then
        allowedRange = math.max(allowedRange, combatConfig.loopShootRange or allowedRange)
        sightMultiplier = math.max(sightMultiplier, combatConfig.loopSightRangeMultiplier or sightMultiplier)
        blindRange = combatConfig.loopBlindShootRange or allowedRange
    elseif directAttackMode then
        allowedRange = math.max(allowedRange, combatConfig.attackShootRange or allowedRange)
        sightMultiplier = math.max(sightMultiplier, combatConfig.attackSightRangeMultiplier or sightMultiplier)
        blindRange = combatConfig.attackBlindShootRange or allowedRange
    elseif flameFocusMode then
        allowedRange = 32
        sightMultiplier = 1
    end
    local canSeeTarget = distance <= allowedRange
    if not canSeeTarget then
        local allowBlindShot = blindRange
            and (loopModeActive or directAttackMode or sentryModeActive or targetIndoors or followShootThroughWalls)
        if allowBlindShot then
            canSeeTarget = distance <= blindRange
        end
        if not canSeeTarget and hasLineOfSight(origin, targetCharacter, targetPart) then
            canSeeTarget = distance <= (allowedRange * sightMultiplier)
        end
    end
    if not canSeeTarget then
        return
    end

    local leadTimeMax = combatConfig.leadTimeMax
    local leadScale = combatConfig.leadScale
    if loopModeActive then
        leadTimeMax = math.max(leadTimeMax, combatConfig.loopLeadTimeMax or leadTimeMax)
        leadScale = math.max(leadScale, combatConfig.loopLeadScale or leadScale)
        if targetIndoors then
            leadTimeMax = leadTimeMax + 0.15
            leadScale = leadScale + 0.1
        end
        if fastTarget then
            leadTimeMax = leadTimeMax + 0.2
            leadScale = leadScale + 0.15
        end
        if extremeTarget then
            leadTimeMax = leadTimeMax + 0.35
            leadScale = leadScale + 0.25
        end
        if standDuelTarget then
            leadTimeMax = leadTimeMax + (combatConfig.standDuelLoopLeadTimeBoost or 0.35)
            leadScale = leadScale + (combatConfig.standDuelLoopLeadScaleBoost or 0.24)
        end
        if standDuelExtreme then
            leadTimeMax = leadTimeMax + 0.15
            leadScale = leadScale + 0.08
        end
    elseif directAttackMode then
        leadTimeMax = math.max(leadTimeMax, combatConfig.attackLeadTimeMax or leadTimeMax)
        leadScale = math.max(leadScale, combatConfig.attackLeadScale or leadScale)
        if targetIndoors then
            leadTimeMax = leadTimeMax + 0.08
            leadScale = leadScale + 0.06
        end
        if fastTarget then
            leadTimeMax = leadTimeMax + 0.1
            leadScale = leadScale + 0.08
        end
        if extremeTarget then
            leadTimeMax = leadTimeMax + 0.18
            leadScale = leadScale + 0.12
        end
        if standDuelTarget then
            leadTimeMax = leadTimeMax + (combatConfig.standDuelAttackLeadTimeBoost or 0.16)
            leadScale = leadScale + (combatConfig.standDuelAttackLeadScaleBoost or 0.12)
        end
        if standDuelExtreme then
            leadTimeMax = leadTimeMax + 0.06
            leadScale = leadScale + 0.04
        end
    end
    local aimPosition
    if flameFocusMode and targetHead then
        aimPosition = targetHead.Position + Vector3.new(0, 0.05, 0)
    else
        aimPosition = calculateLeadAim(
            origin,
            targetPart.Position,
            targetVelocity,
            distance,
            allowedRange,
            leadTimeMax,
            leadScale
        )
    end

    if circleShotMode then
        local circleProfile = sentryModeActive and "sentry" or "attack"
        applyLoopStrafeAimMovement(playerHRP, targetHRP, aimPosition, targetIndoors, target.UserId, circleProfile, isCalmStandCommandActive())
        origin = playerHRP.Position
        distance = (targetPart.Position - origin).Magnitude
        aimPosition = calculateLeadAim(
            origin,
            targetPart.Position,
            targetVelocity,
            distance,
            allowedRange,
            leadTimeMax,
            leadScale
        )
    end

    if flameFocusMode then
        local flameTool = getGunToolByKey("flamethrower")
        if not flameTool then
            local backpack = Player and Player:FindFirstChild("Backpack")
            flameTool = playerChar:FindFirstChild(FLAME_TOOL_NAME) or (backpack and backpack:FindFirstChild(FLAME_TOOL_NAME))
        end
        if flameTool then
            if not tryReloadTool(flameTool) then
                if flameTool.Parent ~= playerChar then
                    flameTool.Parent = playerChar
                end
                applyStandMovementCFrame(playerHRP, CFrame.lookAt(playerHRP.Position, aimPosition))
                if (now - (lastFlameActivateAt or 0)) >= FLAME_HOLD_CLICK_INTERVAL then
                    pcall(function()
                        flameTool:Activate()
                    end)
                    lastFlameActivateAt = now
                end
            end
        end
    else
        local toolsToFire = collectGunTools()
        if #toolsToFire == 0 then
            markCombatLoadoutDemand(3.2)
            requestCombatAttackPrime(target, true)
            reloadTool()
            toolsToFire = collectGunTools()
            if #toolsToFire == 0 then
                return
            end
        elseif (now - lastShootAt) >= 0.65 then
            requestCombatAttackPrime(target, false)
        end
        local shotsPerTool = effectiveShots
        local toolLimit = #toolsToFire
        if powerModeActive and toolLimit > 0 then
            toolLimit = math.min(toolLimit, math.max(1, EquipGunCount or 2))
            local totalBudget = getPowerModeShotBudget(
                distance,
                loopModeActive,
                directAttackMode,
                sentryModeActive,
                targetIndoors,
                standDuelTarget,
                standDuelExtreme
            )
            shotsPerTool = clamp(math.floor((totalBudget / toolLimit) + 0.5), 1, effectiveShots)
        end
        for i, tool in ipairs(toolsToFire) do
            if powerModeActive and i > toolLimit then
                break
            end
            local handle = getShootHandle(tool)
            if handle then
                if tryReloadTool(tool) then
                    continue
                end
                fireToolAtTarget(tool, targetPart, shotsPerTool, aimPosition)
            end
        end
    end
end)

RunService.Heartbeat:Connect(function()
    if not getgenv().enabled then
        return
    end
    if postResetCombatRecoveryActive or buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress then
        return
    end
    if bringonly or takeonly or toDeliveryActive or autosaveActive or isCurrentlyGrabbing() then
        return
    end
    if flameModeActive and flameModeTargetUserId and lockedTarget and lockedTarget.UserId == flameModeTargetUserId then
        return
    end
    if smiteCommandInProgress then
        return
    end

    local lp = game.Players.LocalPlayer
    local char = lp and lp.Character
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    if not hrp then
        return
    end

    local koValue = char:FindFirstChild("BodyEffects") and char.BodyEffects:FindFirstChild("K.O")
    if not koValue or not koValue.Value then
        if followFireInProgress then
            return
        end
        local now = os.clock()
        local followCooldownFloor = getgenv().enabled and (ownerFollowShotCooldown or 0.045) or (standTuning.minFollowShotCooldown or 0.06)
        local followCooldown = math.max(followShotCooldown or 0, followCooldownFloor)
        if (now - lastFollowShotAt) < followCooldown then
            return
        end
        local centerPos = nil

        if targetPlayer and targetPlayer.Character then
            local ownerHRP = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
            if ownerHRP then
                centerPos = ownerHRP.Position
                lastOwnerPosition = centerPos
            end
        end
        if not centerPos then
            centerPos = lastOwnerPosition or hrp.Position
        end
        if not centerPos then
            return
        end

        local targets = collectGridTargets(centerPos)
        if #targets == 0 then
            return
        end

        local toolsToFire = {}
        local seen = {}
        for _, gunKey in ipairs(Guns) do
            local tool = getGunToolByKey(gunKey)
            if tool and not seen[tool] then
                seen[tool] = true
                table.insert(toolsToFire, tool)
            end
        end
        if #toolsToFire == 0 then
            toolsToFire = collectGunTools()
        end
        if #toolsToFire == 0 then
            markCombatLoadoutDemand(3.2)
            local backpack = lp and lp:FindFirstChild("Backpack")
            if equipRespawnCombatLoadout(char, backpack) then
                reloadTool()
                toolsToFire = collectGunTools()
            end
        end
        if #toolsToFire == 0 then
            postResetCombatRecoveryActive = true
            postResetCombatRecoveryUntil = math.max(postResetCombatRecoveryUntil or 0, os.clock() + 2.5)
            requestImmediateCombatLoadoutPrime()
            return
        end

        followFireInProgress = true
        lastFollowShotAt = now
        local followBurstScale = getNetworkBurstScale(true)
        local activeFollowShots = getgenv().enabled and math.max(followShotsPerTick or 1, ownerFollowShotsPerTick or 2) or (followShotsPerTick or 1)
        local activeFollowSpacing = getgenv().enabled and math.min(followGunSpacing or 0.01, ownerFollowGunSpacing or 0.006) or (followGunSpacing or 0.01)
        local followBurst = clamp(
            math.floor((activeFollowShots * followBurstScale) + 0.5),
            1,
            math.max(1, (standTuning.maxBurstShots or 6) - 2)
        )
        local followTargetLimit = math.max(
            1,
            math.min(
                #targets,
                math.floor((followMaxTargets * math.max(networkTuning.minFollowTargetScale or 0.5, followBurstScale)) + 0.5)
            )
        )
        task.spawn(function()
            local ok, err = pcall(function()
                for index, targetPlayer in ipairs(targets) do
                    if index > followTargetLimit then
                        break
                    end
                    local targetChar = targetPlayer.Character
                    local targetPart = targetChar and targetChar:FindFirstChild("Head")
                    if targetPart and isAliveCharacter(targetChar) then
                        for _, tool in ipairs(toolsToFire) do
                            fireToolAtTarget(tool, targetPart, followBurst)
                            if activeFollowSpacing > 0 then
                                task.wait(activeFollowSpacing)
                            end
                        end
                    end
                end
            end)
            followFireInProgress = false
            if not ok then
                warn(err)
            end
        end)
    end
end)

Player = game.Players.LocalPlayer
Character = Player.Character or Player.CharacterAdded:Wait()
humanoid = Character:FindFirstChildOfClass("Humanoid")
root = Character:FindFirstChild("HumanoidRootPart")

Player.CharacterAdded:Connect(function(char)
    Character = char
    humanoid = char:WaitForChild("Humanoid")
    root = char:WaitForChild("HumanoidRootPart")
end)

function getEquippedGuns()
    local guns = {}
    local char = Player.Character
    if char then
        for _, tool in ipairs(char:GetChildren()) do
            if tool:IsA("Tool") then
                table.insert(guns, tool)
            end
        end
    end
    return guns
end

function getAmmoCount(gunName)
    local inventory = Player.DataFolder.Inventory
    local ammo = inventory:FindFirstChild(gunName)
    if ammo then
        return tonumber(ammo.Value)
    end
    return nil
end

function hasGun(toolName)
    local player = Player
    if not player then return false end
    
    local backpack = player:FindFirstChild("Backpack")
    if backpack then
        for _, item in ipairs(backpack:GetChildren()) do
            if item:IsA("Tool") and item.Name == toolName then
                return true
            end
        end
    end
    
    local character = player.Character
    if character then
        for _, item in ipairs(character:GetChildren()) do
            if item:IsA("Tool") and item.Name == toolName then
                return true
            end
        end
    end
    
    return false
end

local function hasMissingConfiguredGuns()
    for i = 1, #Guns do
        local gunKey = Guns[i]
        if DisabledGuns[gunKey] then
            continue
        end
        local gunInfo = gunData[gunKey]
        if gunInfo and not hasGun(gunInfo.toolName) then
            return true
        end
    end
    return false
end

resetRespawnFireState = function()
    followFireInProgress = false
    lastShootAt = 0
    lastFollowShotAt = 0
    lastFlameActivateAt = 0
    lastCombatShotSuccessAt = 0
end

local function markCombatLoadoutDemand(duration)
    local now = os.clock()
    combatLoadoutDemandUntil = math.max(combatLoadoutDemandUntil or 0, now + (duration or 2.6))
end

local function clearCombatLoadoutDemand()
    combatLoadoutDemandUntil = 0
end

local function clearStaleLoadoutFlags(force)
    local now = os.clock()
    local stale = force or (
        (buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress or immediateLoadoutPrimeInProgress)
        and (lastImmediateLoadoutPrimeRequestAt or 0) > 0
        and (now - lastImmediateLoadoutPrimeRequestAt) > 7
    )
    if not stale then
        return false
    end
    buyingInProgress = false
    buyingGunInProgress = false
    buyingMaskInProgress = false
    buyingArmorInProgress = false
    buyingVehicleInProgress = false
    immediateLoadoutPrimeInProgress = false
    return true
end

hasUsableCombatLoadout = function(currentCharacter, backpack)
    if flameModeActive and flameModeTargetUserId and lockedTarget and lockedTarget.UserId == flameModeTargetUserId then
        return (currentCharacter and currentCharacter:FindFirstChild(FLAME_TOOL_NAME)) ~= nil
            or (backpack and backpack:FindFirstChild(FLAME_TOOL_NAME)) ~= nil
    end

    return #collectGunTools() > 0
end

equipRespawnCombatLoadout = function(currentCharacter, backpack)
    if flameModeActive and flameModeTargetUserId and lockedTarget and lockedTarget.UserId == flameModeTargetUserId then
        local flameTool = (currentCharacter and currentCharacter:FindFirstChild(FLAME_TOOL_NAME))
            or (backpack and backpack:FindFirstChild(FLAME_TOOL_NAME))
        if flameTool and currentCharacter and flameTool.Parent ~= currentCharacter then
            flameTool.Parent = currentCharacter
        elseif not flameTool then
            equipTool(FLAME_TOOL_NAME)
        end
        return hasUsableCombatLoadout(currentCharacter, backpack)
    end

    equipConfiguredGuns()
    return hasUsableCombatLoadout(currentCharacter, backpack)
end

local function equipConfiguredGuns()
    for i = 1, #Guns do
        local gunKey = Guns[i]
        if DisabledGuns[gunKey] then
            continue
        end
        local gunInfo = gunData[gunKey]
        if gunInfo and hasGun(gunInfo.toolName) then
            equipTool(gunInfo.toolName)
        end
    end
    reloadTool()
end

local function buyMissingConfiguredGunsNow()
    clearStaleLoadoutFlags(false)
    markCombatLoadoutDemand(4.2)
    if immediateLoadoutPrimeInProgress then
        local backpack = Player and Player:FindFirstChild("Backpack")
        return hasUsableCombatLoadout(Player and Player.Character, backpack)
    end
    if buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress then
        local backpack = Player and Player:FindFirstChild("Backpack")
        return hasUsableCombatLoadout(Player and Player.Character, backpack)
    end

    local char = Player and Player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (char and root and humanoid and humanoid.Health > 0) then
        return false
    end

    immediateLoadoutPrimeInProgress = true
    local prevBuying = buyingInProgress
    local prevGunBuying = buyingGunInProgress
    local success = false

    local ok = pcall(function()
        for i = 1, #Guns do
            local gunKey = Guns[i]
            if DisabledGuns[gunKey] then
                continue
            end

            local gunInfo = gunData[gunKey]
            if gunInfo and not hasGun(gunInfo.toolName) then
                buyingInProgress = true
                buyingGunInProgress = true

                local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
                local shopPart = findShopItem(shopFolder, gunInfo.shopName, {ammo = false})
                local clickDetector = shopPart and shopPart:FindFirstChildWhichIsA("ClickDetector", true)
                local shopBase = shopPart and getShopBasePart(shopPart, clickDetector)

                if clickDetector and shopBase then
                    withNoclip(function()
                        local buyAttempts = 0
                        while not hasGun(gunInfo.toolName) and buyAttempts < 12 do
                            if humanoid then
                                humanoid:UnequipTools()
                            end
                            safeTeleportToShop(root, shopBase)
                            task.wait(0.05)
                            getgenv().fireclickdetector(clickDetector)
                            task.wait(0.12)
                            buyAttempts += 1
                        end
                    end)
                end

                buyingGunInProgress = prevGunBuying
                buyingInProgress = prevBuying

                if hasGun(gunInfo.toolName) then
                    equipTool(gunInfo.toolName)
                    buyAmmoForGun(gunInfo.toolName, AmmoPurchaseCount)
                end
            end
        end

        equipConfiguredGuns()
        local backpack = Player and Player:FindFirstChild("Backpack")
        success = hasUsableCombatLoadout(char, backpack)
        if success then
            clearCombatLoadoutDemand()
        end
    end)

    buyingGunInProgress = prevGunBuying
    buyingInProgress = prevBuying
    immediateLoadoutPrimeInProgress = false
    requestIdleVoidReturn(0.06)

    if not ok then
        return false
    end

    return success
end

requestImmediateCombatLoadoutPrime = function()
    lastImmediateLoadoutPrimeRequestAt = os.clock()
    markCombatLoadoutDemand(3.4)
    if immediateLoadoutPrimeInProgress then
        clearStaleLoadoutFlags(false)
        if immediateLoadoutPrimeInProgress then
            return
        end
    end

    task.spawn(function()
        task.wait(0.03)
        buyMissingConfiguredGunsNow()
    end)
end

requestOwnerFollowLoadoutPrimeBurst = function()
    task.spawn(function()
        for attempt = 1, 6 do
            if hardStop or not getgenv().enabled then
                return
            end
            local currentCharacter = Player and Player.Character
            local currentBackpack = Player and Player:FindFirstChild("Backpack")
            if currentCharacter then
                equipRespawnCombatLoadout(currentCharacter, currentBackpack)
            end
            if hasUsableCombatLoadout(currentCharacter, currentBackpack) then
                postResetCombatRecoveryActive = false
                postResetCombatRecoveryUntil = 0
                equipConfiguredGuns()
                reloadTool()
                resetRespawnFireState()
                resetCombatFireWindow()
                return
            end
            requestImmediateCombatLoadoutPrime()
            task.wait(attempt == 1 and 0.03 or (attempt <= 3 and 0.12 or 0.2))
        end
        if getgenv().enabled and not hardStop then
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
            equipConfiguredGuns()
            reloadTool()
            resetRespawnFireState()
            resetCombatFireWindow()
        end
    end)
end

function requestPostCarryCombatRecovery(target, forceBurst)
    if hardStop then
        return
    end

    local now = os.clock()
    local minInterval = forceBurst and 0.12 or 0.22
    if (now - (lastCarryCombatRecoveryAt or 0)) < minInterval then
        return
    end
    lastCarryCombatRecoveryAt = now
    lastCarryReleaseFlushAt = now

    markCombatLoadoutDemand(forceBurst and 3.2 or 2.1)

    task.spawn(function()
        if hardStop then
            return
        end

        followFireInProgress = false
        resetRespawnFireState()
        resetCombatFireWindow()
        if followState then
            followState.currentTargetCharacter = nil
            followState.lastTargetPosition = nil
            followState.targetVelocity = Vector3.zero
            followState.lastUpdate = os.clock()
            followState.lastTargetWasKO = nil
            followState.lastTargetWasDead = nil
            if target and target.UserId then
                followState.currentTargetId = target.UserId
            end
        end
        lastCombatPrimeRefreshAt = 0
        combatPrimeWindowUntil = math.max(combatPrimeWindowUntil or 0, os.clock() + (forceBurst and 1.05 or 0.55))

        pcall(function()
            ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
        end)
        task.wait(forceBurst and 0.025 or 0.04)
        if not (bringonly or takeonly or toDeliveryActive or autosaveActive) then
            pcall(function()
                ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
            end)
        end

        local currentCharacter = Player and Player.Character
        local currentBackpack = Player and Player:FindFirstChild("Backpack")
        if currentCharacter then
            equipRespawnCombatLoadout(currentCharacter, currentBackpack)
        else
            equipConfiguredGuns()
        end
        reloadTool()
        requestImmediateCombatLoadoutPrime()
        if getgenv().enabled then
            requestOwnerFollowLoadoutPrimeBurst()
        end
    end)
end

function requestCombatAttackPrime(target, forceBurst)
    if hardStop then
        return
    end

    if not (bringonly or takeonly or toDeliveryActive or autosaveActive) then
        requestPostCarryCombatRecovery(target, forceBurst and true or false)
    end

    local now = os.clock()
    local targetUserId = target and target.UserId or nil
    if targetUserId ~= lastCombatPrimeTargetUserId then
        lastCombatPrimeTargetUserId = targetUserId
        lastCombatPrimeRefreshAt = 0
    end

    local refreshCooldown = forceBurst and 0.08 or 0.18
    if (now - (lastCombatPrimeRefreshAt or 0)) < refreshCooldown then
        return
    end

    lastCombatPrimeRefreshAt = now
    combatPrimeWindowUntil = math.max(combatPrimeWindowUntil or 0, now + (forceBurst and 1.2 or 0.75))
    markCombatLoadoutDemand(forceBurst and 3.2 or 2.4)

    resetRespawnFireState()
    resetCombatFireWindow()

    task.spawn(function()
        local attempts = forceBurst and 5 or 3
        for attempt = 1, attempts do
            if hardStop then
                return
            end

            local currentCharacter = Player and Player.Character
            local currentBackpack = Player and Player:FindFirstChild("Backpack")

            if currentCharacter then
                equipRespawnCombatLoadout(currentCharacter, currentBackpack)
            else
                equipConfiguredGuns()
            end

            reloadTool()
            requestImmediateCombatLoadoutPrime()

            if hasUsableCombatLoadout(currentCharacter, currentBackpack) and attempt >= 2 then
                return
            end

            task.wait(attempt == 1 and 0.03 or (attempt <= 3 and 0.08 or 0.14))
        end
    end)
end

function hasActiveCombatRecoveryTask()
    return not hardStop and (
        getgenv().enabled
        or getgenv().enabled1
        or stand2Active
        or flameModeActive
        or smiteCommandInProgress
        or stomponly
        or getgenv().downonly
        or opkill
        or killall
        or lockedTarget ~= nil
        or lockedTargetUserId ~= nil
        or sentrytarget ~= nil
        or #ragebottargets > 0
    )
end

function getCombatRecoveryTarget()
    if lockedTarget and lockedTarget.Character then
        return lockedTarget
    end
    if sentrytarget and sentrytarget.Character then
        return sentrytarget
    end
    if stand2CurrentTarget and stand2CurrentTarget.Character then
        return stand2CurrentTarget
    end
    if skyTarget and skyTarget.Character then
        return skyTarget
    end
    if savedTarget5 and savedTarget5.Character then
        return savedTarget5
    end
    if ragebottargets and #ragebottargets > 0 then
        for _, playerTarget in ipairs(ragebottargets) do
            if playerTarget and playerTarget.Character then
                return playerTarget
            end
        end
    end
    if smiteTargetUserId then
        local smiteTargetPlayer = Players:GetPlayerByUserId(smiteTargetUserId)
        if smiteTargetPlayer and smiteTargetPlayer.Character then
            return smiteTargetPlayer
        end
    end
    return nil
end

function bootstrapCombatAfterRespawn(expectedCharacter)
    local bootstrapId = os.clock()
    lastRespawnCombatBootstrapAt = bootstrapId

    task.spawn(function()
        for attempt = 1, 14 do
            if lastRespawnCombatBootstrapAt ~= bootstrapId or hardStop then
                return
            end

            local localPlayer = Players.LocalPlayer
            local currentCharacter = localPlayer and localPlayer.Character
            if not currentCharacter or currentCharacter ~= expectedCharacter then
                return
            end

            local humanoid = currentCharacter:FindFirstChildOfClass("Humanoid") or currentCharacter:FindFirstChild("Humanoid")
            local backpack = localPlayer and localPlayer:FindFirstChild("Backpack")
            if humanoid and humanoid.Health > 0 then
                clearStaleLoadoutFlags(attempt >= 6)
                resetFollowPrediction()
                resetRespawnFireState()
                resetCombatFireWindow()
                pcall(function()
                    ReplicatedStorage.MainEvent:FireServer("Grabbing", false)
                end)

                if backpack then
                    equipRespawnCombatLoadout(currentCharacter, backpack)
                else
                    equipConfiguredGuns()
                end
                reloadTool()

                if not hasUsableCombatLoadout(currentCharacter, backpack) and hasMissingConfiguredGuns() then
                    requestImmediateCombatLoadoutPrime()
                end

                if hasActiveCombatRecoveryTask() then
                    postResetCombatRecoveryActive = false
                    postResetCombatRecoveryUntil = 0
                    postResetLoadoutGraceUntil = 0

                    local primaryTarget = getCombatRecoveryTarget()
                    if primaryTarget then
                        requestCombatAttackPrime(primaryTarget, true)
                    else
                        requestOwnerFollowLoadoutPrimeBurst()
                    end

                    if hasUsableCombatLoadout(currentCharacter, backpack) and attempt >= 3 then
                        return
                    end
                elseif hasUsableCombatLoadout(currentCharacter, backpack) and attempt >= 2 then
                    return
                end
            end

            task.wait(attempt <= 3 and 0.12 or (attempt <= 8 and 0.2 or 0.32))
        end
    end)
end

primeCombatLoadoutAfterRespawn = function(expectedCharacter)
    postResetLoadoutGraceUntil = math.max(postResetLoadoutGraceUntil, os.clock() + 2.2)
    local attempts = 0
    local maxAttempts = 18

    local function attemptPrime()
        attempts += 1
        local localPlayer = Players.LocalPlayer
        local currentCharacter = localPlayer and localPlayer.Character
        if not currentCharacter or currentCharacter ~= expectedCharacter or hardStop then
            return
        end

        local currentHumanoid = currentCharacter:FindFirstChildOfClass("Humanoid") or currentCharacter:WaitForChild("Humanoid", 2)
        local backpack = localPlayer:FindFirstChild("Backpack") or localPlayer:WaitForChild("Backpack", 2)
        if not (currentHumanoid and currentHumanoid.Health > 0 and backpack) then
            if attempts < maxAttempts then
                task.delay(0.15, attemptPrime)
            end
            return
        end

        resetRespawnFireState()

        local combatReady = equipRespawnCombatLoadout(currentCharacter, backpack)

        if combatReady then
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
            postResetLoadoutGraceUntil = 0
            reloadTool()
            return
        end

        reloadTool()
        if attempts < maxAttempts then
            task.delay(0.15, attemptPrime)
        end
    end

    task.delay(0.15, attemptPrime)
end

function getNextItemToBuy()
    local char = Player.Character
    if not char then return nil end

    for i = 1, #Guns do
        local gunKey = Guns[i]
        if DisabledGuns[gunKey] then
            continue
        end
        local gunInfo = gunData[gunKey]
        if gunInfo and not hasGun(gunInfo.toolName) then
            return "gun"
        end
    end

    if automaskenabled and not (char:FindFirstChild("[Mask]") or char:FindFirstChild("In-gameMask")) then
        return "mask"
    end

    return nil
end

fired = false

game:GetService("Players").LocalPlayer.CharacterAdded:Connect(function()
    fired = false
end)

nativeFireClickDetector = fireclickdetector

function resolveClickDetector(object)
    if typeof(object) ~= "Instance" then return nil end
    if object:IsA("ClickDetector") then
        return object
    end
    return object:FindFirstChildWhichIsA("ClickDetector", true)
end

function manualFireClickDetector(clickDetector)
    if not fired then
        fired = true
        game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.E, false, game)
    end

    local localChar = game:GetService("Players").LocalPlayer.Character
    if localChar and localChar:FindFirstChildOfClass("Tool") then
        local humanoid = localChar:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid:UnequipTools()
        end
    end

    local old_cd_parent = clickDetector.Parent

    local stub_part = Instance.new("Part")
    stub_part.Transparency = 1
    stub_part.Size = Vector3.new(30, 30, 30)
    stub_part.Anchored = true
    stub_part.CanCollide = false
    stub_part.Parent = workspace

    clickDetector.Parent = stub_part
    clickDetector.MaxActivationDistance = math.huge

    local connection = game:GetService("RunService").Heartbeat:Connect(function()
        stub_part.CFrame = workspace.Camera.CFrame * CFrame.new(0, 0, -20) * CFrame.new(workspace.Camera.CFrame.LookVector)
        game:GetService("VirtualUser"):ClickButton1(Vector2.new(20, 20), workspace:FindFirstChildOfClass("Camera").CFrame)
    end)

    clickDetector.MouseClick:Once(function()
        connection:Disconnect()
        clickDetector.Parent = old_cd_parent
        stub_part:Destroy()
    end)

    task.delay(3, function()
        connection:Disconnect()
        clickDetector.Parent = old_cd_parent
        stub_part:Destroy()
    end)
end

function tryNativeClick(clickDetector)
    if not nativeFireClickDetector then
        return false
    end
    local ok = pcall(nativeFireClickDetector, clickDetector)
    return ok
end

getgenv().fireclickdetector = function(object)
    local clickDetector = resolveClickDetector(object)
    if not clickDetector then return end

    if tryNativeClick(clickDetector) then
        return
    end

    manualFireClickDetector(clickDetector)
end

function getShopBasePart(item, clickDetector)
    if clickDetector and clickDetector.Parent and clickDetector.Parent:IsA("BasePart") then
        return clickDetector.Parent
    end
    if not item then
        return nil
    end
    local head = item:FindFirstChild("Head")
    if head and head:IsA("BasePart") then
        return head
    end
    return item:FindFirstChildWhichIsA("BasePart", true)
end

function findShopItem(shopFolder, fullName, opts)
    if not shopFolder or not fullName then
        return nil
    end
    local exact = shopFolder:FindFirstChild(fullName)
    if exact then
        return exact
    end
    local bracket = fullName:match("%[(.-)%]")
    if not bracket then
        return nil
    end
    local wantAmmo = opts and opts.ammo
    for _, child in ipairs(shopFolder:GetChildren()) do
        if child.Name:find(bracket, 1, true) then
            if wantAmmo ~= nil then
                local isAmmo = child.Name:find("Ammo", 1, true) ~= nil
                if wantAmmo and not isAmmo then
                    continue
                end
                if (not wantAmmo) and isAmmo then
                    continue
                end
            end
            return child
        end
    end
    return nil
end

armorItems = {
    standard = {
        name = "[High-Medium Armor] - $2589",
        position = Vector3.new(-934.025, -28.15, 570.55),
    },
    fire = {
        name = "[Fire Armor] - $4501",
        position = Vector3.new(-934.028, -4.872, 151.994),
    }
}

function getArmorValue()
    local char = Player.Character
    local bodyEffects = char and char:FindFirstChild("BodyEffects")
    local armor = bodyEffects and bodyEffects:FindFirstChild("Armor")
    if armor and typeof(armor.Value) == "number" then
        return armor.Value
    end
    return 0
end

function hasFireArmor()
    local char = Player.Character
    local bodyEffects = char and char:FindFirstChild("BodyEffects")
    if not bodyEffects then
        return false
    end
    local fields = {"FireResist", "FireProtection", "FireArmor", "FireProof"}
    for _, fieldName in ipairs(fields) do
        local field = bodyEffects:FindFirstChild(fieldName)
        if field then
            if typeof(field.Value) == "boolean" and field.Value then
                return true
            end
            if typeof(field.Value) == "number" and field.Value > 0 then
                return true
            end
        end
    end
    local charFire = char:FindFirstChild("FireArmor") or char:FindFirstChild("FireProtection")
    if charFire then
        return true
    end
    return false
end

function purchaseArmor(itemInfo)
    if not itemInfo then
        return false
    end
    local char = Player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (root and humanoid and humanoid.Health > 0) then
        return false
    end
    if buyingGunInProgress or buyingInProgress or buyingMaskInProgress or buyingArmorInProgress then
        return false
    end

    local now = os.clock()
    if now - lastArmorPurchase < 1 then
        return false
    end

    local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
    local armorItem = shopFolder and findShopItem(shopFolder, itemInfo.name, {ammo = false})
    local clickDetector = armorItem and armorItem:FindFirstChildWhichIsA("ClickDetector", true)
    local shopBase = getShopBasePart(armorItem, clickDetector)
    if not clickDetector or not shopBase then
        return false
    end

    local prevBuying = buyingInProgress
    buyingArmorInProgress = true
    buyingInProgress = true

    local success = false
    withNoclip(function()
        for _ = 1, 4 do
            if humanoid then
                humanoid:UnequipTools()
            end
            safeTeleportToShop(root, shopBase)
            getgenv().fireclickdetector(clickDetector)
            task.wait(0.25)
            if getArmorValue() >= ArmorThreshold then
                success = true
                break
            end
        end
    end)

    buyingInProgress = prevBuying
    buyingArmorInProgress = false
    requestIdleVoidReturn(0.06)
    if success then
        lastArmorPurchase = os.clock()
    end
    return success
end

function buyAmmoForGun(gunName, times)
    if not gunName or SkipAmmoFor[gunName] or not AmmoMap then
        return
    end
    if not hasGun(gunName) then
        return
    end
    local ammoItemName = AmmoMap[gunName]
    if not ammoItemName then
        return
    end
    local char = Player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (root and humanoid and humanoid.Health > 0) then
        return
    end

    local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
    local ammoItem = findShopItem(shopFolder, ammoItemName, {ammo = true})
    if not ammoItem then
        return
    end

    local clickDetector = ammoItem:FindFirstChildWhichIsA("ClickDetector", true)
    local shopPart = getShopBasePart(ammoItem, clickDetector)
    if not (clickDetector and shopPart) then
        return
    end

    local prevBuying = buyingInProgress
    buyingInProgress = true
    local buyCount = times or AmmoPurchaseCount
    withNoclip(function()
        for _ = 1, buyCount do
            if humanoid then
                humanoid:UnequipTools()
            end
            safeTeleportToShop(root, shopPart)
            getgenv().fireclickdetector(clickDetector)
            task.wait(0.1)
        end
    end)
    buyingInProgress = prevBuying
    reloadTool()
    requestIdleVoidReturn(0.06)
end

task.spawn(function()
    local buyStateStartedAt = 0
    while true do
        local now = os.clock()
        local buyStateActive = buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress or immediateLoadoutPrimeInProgress
        if buyStateActive then
            if buyStateStartedAt == 0 then
                buyStateStartedAt = now
            elseif (now - buyStateStartedAt) > 7 then
                clearStaleLoadoutFlags(true)
                buyStateStartedAt = 0
            end
        else
            buyStateStartedAt = 0
            local char = Player and Player.Character
            local humanoid = char and char:FindFirstChildOfClass("Humanoid")
            local backpack = Player and Player:FindFirstChild("Backpack")
            if (combatLoadoutDemandUntil or 0) > now
                and char and humanoid and humanoid.Health > 0
                and not hasUsableCombatLoadout(char, backpack)
                and hasMissingConfiguredGuns()
                and (now - (lastImmediateLoadoutPrimeRequestAt or 0)) > 0.45 then
                requestImmediateCombatLoadoutPrime()
            elseif (combatLoadoutDemandUntil or 0) <= now and not hasMissingConfiguredGuns() then
                clearCombatLoadoutDemand()
            end
        end
        task.wait(0.2)
    end
end)

task.spawn(function()
    while true do
        task.wait(0.35)

        if hardStop or not hasActiveCombatRecoveryTask() then
            continue
        end
        if bringonly or takeonly or toDeliveryActive or autosaveActive or isCurrentlyGrabbing() then
            continue
        end
        if followFireInProgress or buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress or buyingVehicleInProgress then
            continue
        end

        local localPlayer = Players.LocalPlayer
        local currentCharacter = localPlayer and localPlayer.Character
        local humanoid = currentCharacter and currentCharacter:FindFirstChildOfClass("Humanoid")
        local backpack = localPlayer and localPlayer:FindFirstChild("Backpack")
        if not (currentCharacter and humanoid and humanoid.Health > 0 and backpack) then
            continue
        end

        if postResetCombatRecoveryActive and hasUsableCombatLoadout(currentCharacter, backpack) then
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
            postResetLoadoutGraceUntil = 0
            resetRespawnFireState()
            resetCombatFireWindow()
            equipRespawnCombatLoadout(currentCharacter, backpack)
            reloadTool()
        end

        if not hasUsableCombatLoadout(currentCharacter, backpack) and hasMissingConfiguredGuns() then
            markCombatLoadoutDemand(3.4)
            requestImmediateCombatLoadoutPrime()
            continue
        end

        local now = os.clock()
        local silenceWindow = (lastCombatShotSuccessAt or 0) > 0 and (now - (lastCombatShotSuccessAt or 0)) or math.huge
        local recentRespawnBootstrap = (now - (lastRespawnCombatBootstrapAt or 0)) < 5.5
        if silenceWindow < 2.4 and not recentRespawnBootstrap then
            continue
        end
        if (now - (lastCombatRecoveryWatchdogAt or 0)) < 1.15 then
            continue
        end

        local recoveryTarget = getCombatRecoveryTarget()
        if recoveryTarget or getgenv().enabled then
            lastCombatRecoveryWatchdogAt = now
            resetFollowPrediction()
            resetRespawnFireState()
            resetCombatFireWindow()
            equipRespawnCombatLoadout(currentCharacter, backpack)
            reloadTool()
            if recoveryTarget then
                requestCombatAttackPrime(recoveryTarget, true)
            else
                requestOwnerFollowLoadoutPrimeBurst()
            end
        end
    end
end)

-- FIXED GUN BUYING LOOP (NOW ACTIVATED)
task.spawn(function()
    while true do
        local recoveryMode = postResetCombatRecoveryActive and os.clock() < postResetCombatRecoveryUntil
        task.wait(recoveryMode and 0.05 or 0.2)
        
        local char = Player.Character
        local root = char and char:FindFirstChild("HumanoidRootPart")
        local humanoid = char and char:FindFirstChildOfClass("Humanoid")
        
        if char and root and humanoid and humanoid.Health > 0 and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            if recoveryMode then
                local backpack = Player:FindFirstChild("Backpack")
                if hasUsableCombatLoadout(char, backpack) then
                    resetRespawnFireState()
                    equipRespawnCombatLoadout(char, backpack)
                    postResetCombatRecoveryActive = false
                    postResetCombatRecoveryUntil = 0
                    postResetLoadoutGraceUntil = 0
                    continue
                end

                if os.clock() < postResetLoadoutGraceUntil then
                    continue
                end
            end

            local missingConfiguredGun = false
            for i = 1, #Guns do
                local gunKey = Guns[i]
                if DisabledGuns[gunKey] then
                    continue
                end
                local gunInfo = gunData[gunKey]
                
                if gunInfo then
                    local toolName = gunInfo.toolName
                    
                    if not hasGun(toolName) then
                        missingConfiguredGun = true
                        buyingGunInProgress = true
                        
                        local shopName = gunInfo.shopName
                        local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
                        local shopPart = findShopItem(shopFolder, shopName, {ammo = false})
                        
                        if shopPart then
                            local clickDetector = shopPart:FindFirstChildWhichIsA("ClickDetector", true)
                            local shopBase = getShopBasePart(shopPart, clickDetector)
                            
                            if clickDetector and shopBase then
                                withNoclip(function()
                                    safeTeleportToShop(root, shopBase)
                                    task.wait(0.05)
                                    
                                    local buyAttempts = 0
                                    while not hasGun(toolName) and buyAttempts < 10 do
                                        if humanoid then
                                            humanoid:UnequipTools()
                                        end
                                        
                                        safeTeleportToShop(root, shopBase)
                                        getgenv().fireclickdetector(clickDetector)
                                        task.wait(0.1)
                                        buyAttempts = buyAttempts + 1
                                    end
                                end)
                                
                                if hasGun(toolName) then
                                    task.wait(0.05)
                                    equipTool(toolName)
                                    buyAmmoForGun(toolName, AmmoPurchaseCount)
                                end
                            end
                        end
                        
                        buyingGunInProgress = false
                        requestIdleVoidReturn(0.06)
                        task.wait(recoveryMode and 0.08 or 0.5)
                    end
                end
            end

            if recoveryMode then
                if not missingConfiguredGun and not hasMissingConfiguredGuns() then
                    equipConfiguredGuns()
                    postResetCombatRecoveryActive = false
                    postResetCombatRecoveryUntil = 0
                elseif os.clock() >= postResetCombatRecoveryUntil then
                    postResetCombatRecoveryActive = false
                    postResetCombatRecoveryUntil = 0
                end
            end
        elseif recoveryMode and os.clock() >= postResetCombatRecoveryUntil then
            postResetCombatRecoveryActive = false
            postResetCombatRecoveryUntil = 0
        end
    end
end)

task.spawn(function()
    while true do
        local char = Player.Character
        if char and automaskenabled and not buyingMaskInProgress and not buyingGunInProgress and not buyingInProgress then
            pcall(function()
                local humanoid = char:FindFirstChildOfClass("Humanoid")

                if Player.Backpack:FindFirstChild("[Mask]") or char:FindFirstChild("[Mask]") or char:FindFirstChild("In-gameMask") then 
                    buyingMaskInProgress = false 
                    requestIdleVoidReturn(0.06)
                    return 
                end

                local ShopFolder = workspace:WaitForChild("Ignored"):WaitForChild("Shop")

                local maskItem = ShopFolder:FindFirstChild(
                    (math.random(1, 2) == 1 and "[Skull Mask] - $66" or "[Riot Mask] - $66")
                )
                if not maskItem then return end

                local clickDetector = maskItem:FindFirstChildWhichIsA("ClickDetector", true)
                if not clickDetector then return end

                    buyingMaskInProgress = true
                    local char = Player.Character
                    local root = char:FindFirstChild("HumanoidRootPart")
                    local shopBase = getShopBasePart(maskItem, clickDetector)
                    if not shopBase then return end

                    withNoclip(function()
                        while automaskenabled and char and not (Player.Backpack:FindFirstChild("[Mask]") or char:FindFirstChild("[Mask]")) do
                        local char = Player.Character
                        local root = char:FindFirstChild("HumanoidRootPart")
                        if root then
                            safeTeleportToShop(root, shopBase)
                        end
                        getgenv().fireclickdetector(clickDetector)
                        task.wait(0.1)
                        if not automaskenabled or not char or (Player.Backpack:FindFirstChild("[Mask]") or char:FindFirstChild("[Mask]")) then break end
                    end
                end)

                task.spawn(function()
                    while automaskenabled and char do
                        local char = Player.Character
                        local maskTool = Player.Backpack:FindFirstChild("[Mask]") or char:FindFirstChild("[Mask]")
                        if maskTool then
                            for _, tool in ipairs(char:GetChildren()) do
                                if tool:IsA("Tool") and tool.Name ~= "[Mask]" then
                                    tool.Parent = Player.Backpack
                                end
                            end
                            maskTool.Parent = char
                            maskTool:Activate()
                        end
                        if char:FindFirstChild("In-gameMask") then
                            local equippedMask = char:FindFirstChild("[Mask]")
                            if equippedMask then
                                equippedMask.Parent = Player.Backpack
                            end
                            buyingMaskInProgress = false
                            requestIdleVoidReturn(0.06)
                            break
                        end
                        if not automaskenabled or not char then break end
                        task.wait(standWait(perf.mask))
                    end
                end)
            end)
        end
        task.wait(standWait(perf.mask))
    end
end)

task.spawn(function()
    while true do
        task.wait(ArmorRecheckDelay)
        local char = Player.Character
        local humanoid = char and char:FindFirstChildOfClass("Humanoid")
        local bodyEffects = char and char:FindFirstChild("BodyEffects")
        if not autoArmorEnabled or not (char and humanoid and humanoid.Health > 0 and bodyEffects) then
            continue
        end
        if buyingGunInProgress or buyingInProgress or buyingMaskInProgress or buyingArmorInProgress then
            continue
        end

        local armorValue = getArmorValue()
        local hasFire = hasFireArmor()

        if armorValue < ArmorThreshold then
            purchaseArmor(armorItems.standard)
            armorValue = getArmorValue()
        end

        if autoFireArmorEnabled and not hasFireArmor() then
            purchaseArmor(armorItems.fire)
        end
    end
end)

AmmoMap = {
    ["[Rifle]"]      = "5 [Rifle Ammo] - $273",
    ["[AUG]"]        = "90 [AUG Ammo] - $87",
    ["[Flintlock]"]  = "6 [Flintlock Ammo] - $163",
    ["[LMG]"]        = "200 [LMG Ammo] - $328",
    ["[Double-Barrel SG]"] = "18 [Double-Barrel SG Ammo] - $55",
    ["[Flamethrower]"] = "140 [Flamethrower Ammo] - $1126"
}

-- FIXED AMMO BUYING LOOP
task.spawn(function()
    while true do
        task.wait(3) -- Check ammo every 3 seconds
        
        local char = Player.Character
        if not char then continue end
        
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        local root = char:FindFirstChild("HumanoidRootPart")
        if not (humanoid and root and humanoid.Health > 0) then
            continue
        end
        if buyingGunInProgress or buyingInProgress or buyingMaskInProgress then
            continue
        end
        if getNextItemToBuy() == "gun" then
            continue
        end

        -- Check reserve ammo for configured guns only.
        for _, gunKey in ipairs(Guns) do
            if DisabledGuns[gunKey] then
                continue
            end
            local gunInfo = gunData[gunKey]
            if gunInfo then
                local gunName = gunInfo.toolName
                if not SkipAmmoFor[gunName] then
                    if not hasGun(gunName) then
                        continue
                    end
                    local ammoCount = getAmmoCount(gunName)
                    if ammoCount and ammoCount <= 0 then
                        buyAmmoForGun(gunName, AmmoPurchaseCount)
                    end
                end
            end
        end
    end
end)

task.spawn(function()
    local lastFlameLoadoutCheck = 0
    while true do
        task.wait(0.8)
        if not flameModeActive then
            continue
        end
        local flameConflict = summonTarget
            or bringonly
            or takeonly
            or getgenv().downonly
            or opkill
            or flingonly
            or killall
            or (#ragebottargets > 0)
            or (lockedTarget and flameModeTargetUserId and lockedTarget.UserId ~= flameModeTargetUserId)
        if flameConflict then
            clearFlameModeState()
            continue
        end
        if hardStop then
            continue
        end
        if buyingGunInProgress or buyingInProgress or buyingMaskInProgress or buyingArmorInProgress then
            continue
        end

        local now = os.clock()
        if (now - lastFlameLoadoutCheck) < 1 then
            continue
        end
        lastFlameLoadoutCheck = now

        if flameModeTargetUserId then
            local refreshed = Players:GetPlayerByUserId(flameModeTargetUserId)
            if refreshed and refreshed ~= LocalPlayer and refreshed ~= lockedTarget then
                lockedTarget = refreshed
                lockedTargetUserId = refreshed.UserId
                teleporting = true
                voiding = false
            end
        end

        if not hasGun(FLAME_TOOL_NAME) then
            prepareFlamethrowerLoadout()
            continue
        end

        equipTool(FLAME_TOOL_NAME)
        local ammoCount = getAmmoCount(FLAME_TOOL_NAME)
        if ammoCount and ammoCount <= 40 then
            buyFlamethrowerAmmoForCommand(5)
            equipTool(FLAME_TOOL_NAME)
        end
    end
end)

task.spawn(function()
    while true do
        task.wait(0.05)
        if hardStop then
            continue
        end
        if not flameModeActive then
            continue
        end
        if not (lockedTarget and flameModeTargetUserId and lockedTarget.UserId == flameModeTargetUserId) then
            continue
        end
        if buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress then
            continue
        end

        local targetChar = lockedTarget.Character
        local myChar = LocalPlayer.Character
        local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
        local upperTorso = targetChar and targetChar:FindFirstChild("UpperTorso")
        local bodyEffects = targetChar and targetChar:FindFirstChild("BodyEffects")
        local isKO = bodyEffects and bodyEffects:FindFirstChild("K.O") and bodyEffects["K.O"].Value
        local isSDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value

        if isSDeath then
            local finalName = flameModeTargetName or (lockedTarget and lockedTarget.Name) or "target"
            disableFlameMode(true)
            sendMessage("Flame task finished on " .. finalName .. ".")
            continue
        end

        if isKO and myHRP and upperTorso then
            local now = os.clock()
            if (now - (lastFlameStompAt or 0)) >= 0.18 then
                teleporting = false
                voiding = false
                for _ = 1, 5 do
                    myHRP.AssemblyLinearVelocity = Vector3.zero
                    myHRP.AssemblyAngularVelocity = Vector3.zero
                    myHRP.CFrame = CFrame.new(upperTorso.Position + Vector3.new(0, 3.2, 0))
                    ReplicatedStorage.MainEvent:FireServer("Stomp")
                    task.wait(0.06)
                end
                lastFlameStompAt = os.clock()
                local finalName = flameModeTargetName or (lockedTarget and lockedTarget.Name) or "target"
                disableFlameMode(true)
                sendMessage("Flame task finished on " .. finalName .. ".")
            end
        end
    end
end)

humanoid = Character:FindFirstChild("Humanoid")
bodyEffects = Character and Character:FindFirstChild("BodyEffects")
koValue = bodyEffects and bodyEffects:FindFirstChild("K.O")

lastDamagerName = ""
getgenv().lastHealths = {}
lastSentryTriggerAt = 0
sentryTriggerCooldown = 0.2
sentryAssistWatchers = {}

function resolveSentryAttacker(rawValue)
    if rawValue == nil then
        return nil
    end

    if typeof(rawValue) == "Instance" then
        if rawValue:IsA("Player") then
            return rawValue
        end

        local fromCharacter = Players:GetPlayerFromCharacter(rawValue)
        if fromCharacter then
            return fromCharacter
        end

        local ancestor = rawValue
        for _ = 1, 4 do
            ancestor = ancestor and ancestor.Parent or nil
            if not ancestor then
                break
            end
            local ancestorPlayer = Players:GetPlayerFromCharacter(ancestor)
            if ancestorPlayer then
                return ancestorPlayer
            end
        end
    end

    local rawText = normalizePlayerInput(tostring(rawValue))
    if not rawText or rawText == "" or rawText == "nil" then
        return nil
    end

    local numericUserId = tonumber(rawText)
    if numericUserId then
        local byUserId = findPlayerByUserIdLocal(numericUserId)
        if byUserId then
            return byUserId
        end
    end

    return findPlayerByExactOrPartial(rawText)
end

function resolveSentryAttackerFromCharacter(protectedChar)
    local bodyEffects = protectedChar and protectedChar:FindFirstChild("BodyEffects")
    local lastDamager = bodyEffects and bodyEffects:FindFirstChild("LastDamager")
    if not lastDamager then
        return nil
    end

    return resolveSentryAttacker(lastDamager.Value)
end

function getSentryLastDamagerObject(protectedChar)
    local bodyEffects = protectedChar and protectedChar:FindFirstChild("BodyEffects")
    return bodyEffects and bodyEffects:FindFirstChild("LastDamager") or nil
end

function getSentryDamagerSnapshot(rawValue)
    if rawValue == nil then
        return ""
    end
    if typeof(rawValue) == "Instance" then
        if rawValue:IsA("Player") then
            return "player:" .. tostring(rawValue.UserId)
        end
        return "instance:" .. tostring(rawValue:GetFullName())
    end
    return tostring(rawValue)
end

function triggerSentryAttackOn(attacker)
    if not (getgenv().enabled1 and attacker) then
        return false
    end

    if attacker == LocalPlayer
        or attacker.Name == Owner
        or getgenv().whitelist[attacker.Name]
        or getgenv().protectedwhitelist[attacker.Name] then
        return false
    end

    local now = os.clock()
    if (now - lastSentryTriggerAt) < sentryTriggerCooldown then
        return false
    end

    lastSentryTriggerAt = now
    cancelAttackModes()
    sentrytarget = attacker
    lockedTarget = attacker
    stomponly = true
    teleporting = true
    voiding = false
    lastShootAt = 0
    requestCombatAttackPrime(attacker, true)
    return true
end

function evaluateSentryProtectedPlayer(state, player, char, allowDamagerOnly)
    if not (state and getgenv().enabled1 and player) then
        return false
    end

    local currentPlayer = findPlayerByUserIdLocal(player.UserId) or player
    local currentChar = currentPlayer and currentPlayer.Character or char
    if not currentChar then
        return false
    end

    local lastDamager = getSentryLastDamagerObject(currentChar)
    if not lastDamager then
        return false
    end

    local rawValue = lastDamager.Value
    local snapshot = getSentryDamagerSnapshot(rawValue)
    if snapshot ~= (state.lastDamagerSnapshot or "") then
        state.lastDamagerSnapshot = snapshot
        state.lastDamagerChangedAt = os.clock()
    end

    local attacker = resolveSentryAttacker(rawValue)
    if not attacker then
        return false
    end

    local now = os.clock()
    local recentHealthDrop = state.lastDamageAt and (now - state.lastDamageAt) <= 0.55
    local recentDamagerUpdate = state.lastDamagerChangedAt and (now - state.lastDamagerChangedAt) <= 0.45
    if allowDamagerOnly or recentHealthDrop or recentDamagerUpdate then
        state.lastTriggeredAt = now
        return triggerSentryAttackOn(attacker)
    end

    return false
end

function disconnectSentryAssistCharacterState(state)
    if state.healthConn then
        state.healthConn:Disconnect()
        state.healthConn = nil
    end
    if state.damagerConn then
        state.damagerConn:Disconnect()
        state.damagerConn = nil
    end
    if state.descendantConn then
        state.descendantConn:Disconnect()
        state.descendantConn = nil
    end
    if state.bodyEffectsConn then
        state.bodyEffectsConn:Disconnect()
        state.bodyEffectsConn = nil
    end
    state.lastDamagerSnapshot = nil
    state.lastDamagerChangedAt = nil
    state.lastDamageAt = nil
end

function scheduleSentryAssistEvaluation(state, player, char, delaySeconds, allowDamagerOnly)
    state.evalToken = (state.evalToken or 0) + 1
    local currentToken = state.evalToken

    task.delay(delaySeconds or 0.05, function()
        if sentryAssistWatchers[player.UserId] ~= state or state.evalToken ~= currentToken then
            return
        end
        if not getgenv().enabled1 then
            return
        end

        evaluateSentryProtectedPlayer(state, player, char, allowDamagerOnly)
    end)
end

function attachSentryAssistDamagerWatcher(state, player, char)
    if state.damagerConn then
        state.damagerConn:Disconnect()
        state.damagerConn = nil
    end
    if state.bodyEffectsConn then
        state.bodyEffectsConn:Disconnect()
        state.bodyEffectsConn = nil
    end

    local bodyEffects = char and char:FindFirstChild("BodyEffects")
    local lastDamager = bodyEffects and bodyEffects:FindFirstChild("LastDamager")

    if lastDamager then
        state.lastDamagerSnapshot = getSentryDamagerSnapshot(lastDamager.Value)
        state.damagerConn = lastDamager:GetPropertyChangedSignal("Value"):Connect(function()
            if not getgenv().enabled1 then
                return
            end
            state.lastDamagerChangedAt = os.clock()
            state.lastDamagerSnapshot = getSentryDamagerSnapshot(lastDamager.Value)
            scheduleSentryAssistEvaluation(state, player, char, 0.01, true)
            scheduleSentryAssistEvaluation(state, player, char, 0.08, false)
        end)
        return
    end

    if bodyEffects then
        state.bodyEffectsConn = bodyEffects.ChildAdded:Connect(function(child)
            if child.Name ~= "LastDamager" then
                return
            end
            attachSentryAssistDamagerWatcher(state, player, char)
            state.lastDamagerChangedAt = os.clock()
            scheduleSentryAssistEvaluation(state, player, char, 0.02, true)
        end)
    end
end

function attachSentryAssistCharacter(state, player, char)
    disconnectSentryAssistCharacterState(state)

    local humanoid = char and (char:FindFirstChildOfClass("Humanoid") or char:WaitForChild("Humanoid", 2))
    if not humanoid then
        state.lastHealth = nil
        if char then
            state.descendantConn = char.ChildAdded:Connect(function(child)
                if child:IsA("Humanoid") or child.Name == "BodyEffects" or child.Name == "LastDamager" then
                    attachSentryAssistCharacter(state, player, char)
                end
            end)
        end
        return
    end

    attachSentryAssistDamagerWatcher(state, player, char)
    state.descendantConn = char.DescendantAdded:Connect(function(descendant)
        if descendant.Name == "BodyEffects" or descendant.Name == "LastDamager" then
            attachSentryAssistDamagerWatcher(state, player, char)
        end
    end)

    state.lastHealth = humanoid.Health
    state.healthConn = humanoid.HealthChanged:Connect(function(newHealth)
        local previousHealth = state.lastHealth
        state.lastHealth = newHealth

        if not (getgenv().enabled1 and previousHealth and (newHealth + 0.05 < previousHealth)) then
            return
        end

        state.lastDamageAt = os.clock()
        scheduleSentryAssistEvaluation(state, player, char, 0.02, false)
        scheduleSentryAssistEvaluation(state, player, char, 0.1, false)
    end)
end

bindSentryAssistPlayer = function(player)
    if not player then
        return
    end

    local userId = player.UserId
    local state = sentryAssistWatchers[userId]
    if not state then
        state = {}
        sentryAssistWatchers[userId] = state
    end

    if state.charConn then
        state.charConn:Disconnect()
        state.charConn = nil
    end
    disconnectSentryAssistCharacterState(state)

    state.playerName = player.Name
    state.charConn = player.CharacterAdded:Connect(function(char)
        attachSentryAssistCharacter(state, player, char)
    end)

    if player.Character then
        attachSentryAssistCharacter(state, player, player.Character)
    else
        state.lastHealth = nil
    end
end

unbindSentryAssistPlayer = function(playerOrUserId)
    local userId = typeof(playerOrUserId) == "Instance" and playerOrUserId.UserId or playerOrUserId
    if not userId then
        return
    end

    local state = sentryAssistWatchers[userId]
    if not state then
        return
    end

    if state.charConn then
        state.charConn:Disconnect()
    end
    disconnectSentryAssistCharacterState(state)
    sentryAssistWatchers[userId] = nil
end

task.spawn(function()
    while true do
        if hardStop then
            task.wait(standWait(perf.equip))
            continue
        end
        if Character then
            for _, tool in ipairs(Character:GetChildren()) do
                if tool:IsA("Tool") then
                    tryReloadTool(tool)
                end
            end
        end
        if not smiteCommandInProgress and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            local backpack = localPlayer:FindFirstChild("Backpack")
            if backpack and humanoid and humanoid.Health > 0 and Character then
                local flameEquipOnly = flameModeActive
                    and flameModeTargetUserId
                    and lockedTarget
                    and lockedTarget.UserId == flameModeTargetUserId
                if flameEquipOnly then
                    -- In .f mode keep exactly one equipped gun: Flamethrower.
                    for _, tool in ipairs(Character:GetChildren()) do
                        if isGunTool(tool) and tool.Name ~= FLAME_TOOL_NAME then
                            tool.Parent = backpack
                        end
                    end
                    local flameTool = Character:FindFirstChild(FLAME_TOOL_NAME) or backpack:FindFirstChild(FLAME_TOOL_NAME)
                    if flameTool and flameTool.Parent ~= Character then
                        flameTool.Parent = Character
                    end
                else
                    local equippedCount = 0
                    local equippedNames = {}

                    for _, tool in ipairs(Character:GetChildren()) do
                        if isGunTool(tool) then
                            equippedCount += 1
                            equippedNames[tool.Name] = true
                        end
                    end

                    if equippedCount < EquipGunCount then
                        for _, gunKey in ipairs(Guns) do
                            if DisabledGuns[gunKey] then
                                continue
                            end
                            local gunInfo = gunData[gunKey]
                            if gunInfo then
                                local gunName = gunInfo.toolName
                                if not equippedNames[gunName] then
                                    local gun = backpack:FindFirstChild(gunName)
                                    if gun then
                                        gun.Parent = Character
                                        equippedCount += 1
                                        equippedNames[gunName] = true
                                        if equippedCount >= EquipGunCount then
                                            break
                                        end
                                    end
                                end
                            end
                        end
                    end
                end
            end
        end
        if autodrop then
            ReplicatedStorage.MainEvent:FireServer("DropMoney", "15000")
        end
        if humanoid and koValue and koValue.Value == true then
            if not autoSaveEnabled and not autoPreKOResetPending then
                humanoid.Health = 0
            end
        end
        if shouldSwitch and #ragebottargets > 0 then
            local attempts = 0
            while attempts < #ragebottargets do
                currentTargetIndex = (currentTargetIndex % #ragebottargets) + 1
                local candidate = ragebottargets[currentTargetIndex]
                if candidate and candidate.Character then
                    local bodyEffects = candidate.Character:FindFirstChild("BodyEffects")
                    local isDeath = bodyEffects and bodyEffects:FindFirstChild("SDeath") and bodyEffects["SDeath"].Value
                    if not isDeath then
                        lockedTarget = candidate
                        shouldSwitch = false
                        break
                    end
                end
                attempts += 1
            end
        end
        task.wait(standWait(perf.equip))
    end
end)

task.spawn(function()
    while task.wait(0.2) do
        if getgenv().enabled1 then
            local playersToCheck = collectSentryProtectedPlayers()

            for _, player in ipairs(playersToCheck) do
                local pname = player.Name
                if bindSentryAssistPlayer and not sentryAssistWatchers[player.UserId] then
                    bindSentryAssistPlayer(player)
                end
                local state = sentryAssistWatchers[player.UserId]
                if player and player.Character then
                    local char = player.Character
                    local bodyEffects = char:FindFirstChild("BodyEffects")
                    local lastDamager = bodyEffects and bodyEffects:FindFirstChild("LastDamager")
                    local humanoid = char:FindFirstChildOfClass("Humanoid")

                    if bodyEffects and lastDamager and humanoid then
                        local healthNow = humanoid.Health
                        if state then
                            if state.lastHealth == nil then
                                state.lastHealth = healthNow
                            elseif healthNow + 0.05 < state.lastHealth then
                                state.lastDamageAt = os.clock()
                            end
                            state.lastHealth = healthNow
                            state.lastDamagerSnapshot = getSentryDamagerSnapshot(lastDamager.Value)
                            evaluateSentryProtectedPlayer(state, player, char, false)
                        end
                        if getgenv().lastHealths[pname] == nil then
                            getgenv().lastHealths[pname] = healthNow
                        end

                        if healthNow + 0.05 < getgenv().lastHealths[pname] then
                            getgenv().lastHealths[pname] = healthNow
                            task.wait(0.1)

                            local recheck = char:FindFirstChild("BodyEffects"):FindFirstChild("LastDamager")
                            local attacker = recheck and resolveSentryAttackerFromCharacter(char)
                            if attacker then
                                triggerSentryAttackOn(attacker)
                            end
                        else
                            getgenv().lastHealths[pname] = healthNow
                        end

                        if sentrytarget and sentrytarget.Character then
                            local atkChar = sentrytarget.Character
                            local atkBE = atkChar:FindFirstChild("BodyEffects")
                            local isKO = atkBE and atkBE:FindFirstChild("K.O") and atkBE["K.O"].Value
                            local isSDeath = atkBE and atkBE:FindFirstChild("SDeath") and atkBE["SDeath"].Value

                            if isKO or isSDeath then
                                if lockedTarget == sentrytarget then
                                    lockedTarget = nil
                                end
                                sentrytarget = nil
                                stomponly = false
                                teleporting = false
                                voiding = true
                                reloadTool()
                            end
                        end
                    end
                else
                    getgenv().lastHealths[pname] = nil
                end
            end
        end
    end
end)

task.spawn(function()
    while task.wait(standWait(perf.summon)) do
        if summonTarget and summonTarget.Character and not (buyingInProgress or buyingGunInProgress or buyingMaskInProgress) then
            local lp = Players.LocalPlayer
            if not lp.Character then continue end

            local hrp = lp.Character:FindFirstChild("HumanoidRootPart")
            local thrp = summonTarget.Character:FindFirstChild("HumanoidRootPart")

            if hrp and thrp then
                voiding = false
                teleporting = false
                hrp.Velocity = Vector3.zero
                hrp.RotVelocity = Vector3.zero
                hrp.AssemblyLinearVelocity = Vector3.zero
                hrp.AssemblyAngularVelocity = Vector3.zero

                local offset
                if summonMode == "middle" then
                    offset = CFrame.new(0, 3, 4)
                elseif summonMode == "right" then
                    offset = CFrame.new(3, 3, 0)
                elseif summonMode == "left" then
                    offset = CFrame.new(-3, 3, 0)
                else
                    offset = CFrame.new(0, 3, 4)
                end

                hrp.CFrame = thrp.CFrame * offset

                hrp.Velocity = Vector3.zero
                hrp.RotVelocity = Vector3.zero
                hrp.AssemblyLinearVelocity = Vector3.zero
                hrp.AssemblyAngularVelocity = Vector3.zero
            end
        end
    end
end)

-- Autosave (bring owner to safe position when knocked)
task.spawn(function()
    local lastSaveAt = 0
    local savingActive = false
    local autosaveCooldownUntil = 0
    local autosaveFailures = 0
    local autosaveMaxFailures = 6
    local AUTOSAVE_GRAB_ROUNDS = 9
    local AUTOSAVE_GRAB_HARDLOCK_ROUNDS = 8
    local AUTOSAVE_CARRY_TIMEOUT = 0.78
    local AUTOSAVE_SETTLE_TIMEOUT = 0.44
    local AUTOSAVE_STAND_DISTANCE = 14
    local AUTOSAVE_OWNER_DISTANCE = 16
    local AUTOSAVE_HOVER_HEIGHT = 5.8
    local AUTOSAVE_SETTLE_HEIGHT = 2.8
    local AUTOSAVE_RELEASE_DISTANCE = 5
    local AUTOSAVE_OWNER_PIN_DISTANCE = 4
    local AUTOSAVE_OWNER_PIN_LOOPS = 10
    local AUTOSAVE_POST_RELEASE_PIN_LOOPS = 12
    local AUTOSAVE_OWNER_PIN_WAIT = 0.03
    local AUTOSAVE_RELEASE_ATTEMPTS = 8
    local AUTOSAVE_RELEASE_WAIT = 0.06
    local AUTOSAVE_SUCCESS_COOLDOWN = 1.4
    local AUTOSAVE_FAIL_COOLDOWN = 0.35
    local AUTOSAVE_HARD_FAIL_COOLDOWN = 1.0

    local function canSaveNow()
        return (os.clock() - lastSaveAt) > 0.2
    end

    local function findOwnerPart(ownerChar)
        return ownerChar and (ownerChar:FindFirstChild("UpperTorso") or ownerChar:FindFirstChild("HumanoidRootPart") or ownerChar:FindFirstChild("Torso"))
    end

    local function releaseGrab(ownerChar)
        return releaseGrabReliably(
            function()
                return isHoldingTargetForDelivery(ownerChar)
            end,
            AUTOSAVE_RELEASE_ATTEMPTS,
            AUTOSAVE_RELEASE_WAIT,
            {
                releaseCheck = function()
                    return isCarryReleaseConfirmed(ownerChar)
                end,
            }
        )
    end

    while task.wait(0.05) do
        if not autoSaveEnabled or savingActive then
            continue
        end
        if os.clock() < autosaveCooldownUntil then
            continue
        end
        if toDeliveryActive and not lastToDestination then
            invalidateToDeliveryRun()
            toDeliveryActive = false
            lastToDropCFrame = nil
            pendingGotoTarget = nil
            pendingGotoTargetUserId = nil
            forceBringDrop = false
            resetBringGrabAttemptState()
            clearDeliveryResumeState()
        end
        if toDeliveryActive then
            continue
        end
        if buyingInProgress or buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress then
            continue
        end
        if vehicleMode then
            continue
        end

        local ownerPlr = Players:FindFirstChild(Owner)
        local ownerChar = ownerPlr and ownerPlr.Character
        local ownerBE = ownerChar and ownerChar:FindFirstChild("BodyEffects")
        local ownerKO = ownerBE and ownerBE:FindFirstChild("K.O")
        if not (ownerKO and ownerKO.Value == true) then
            continue
        end

        -- If owner is already at/near the save spot, do nothing (prevents spam)
        local ownerRoot = ownerChar and ownerChar:FindFirstChild("HumanoidRootPart")
        if ownerRoot and (ownerRoot.Position - autoSavePosition).Magnitude < 16 then
            continue
        end

        if not canSaveNow() then
            continue
        end

        local lp = Players.LocalPlayer
        local myChar = lp and lp.Character
        local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
        local myHum = myChar and myChar:FindFirstChildOfClass("Humanoid")
        local ownerPart = findOwnerPart(ownerChar)
        if not (myHRP and myHum and myHum.Health > 0 and ownerPart) then
            continue
        end

        local resumeState = {
            lockedTarget = lockedTarget,
            lockedTargetUserId = lockedTargetUserId,
            autoLocked = autoLocked,
            teleporting = teleporting,
            voiding = voiding,
            summonTarget = summonTarget,
            stomponly = stomponly,
            bringonly = bringonly,
            takeonly = takeonly,
            downonly = getgenv().downonly,
            opkill = opkill,
            flingonly = flingonly,
            killall = killall,
            ragebottargets = copyListRefs(ragebottargets),
            shouldSwitch = shouldSwitch,
            currentTargetIndex = currentTargetIndex,
            skyTarget = skyTarget,
            savedTarget5 = savedTarget5,
            commandSender = commandSender,
            gotoCFrame = gotoCFrame,
            gotoTarget = gotoTarget,
            gotoTargetUserId = gotoTargetUserId,
            pendingGotoTarget = pendingGotoTarget,
            pendingGotoTargetUserId = pendingGotoTargetUserId or (pendingGotoTarget and pendingGotoTarget.UserId) or nil,
            forceBringDrop = forceBringDrop,
        }

        local function restoreAfterAutosave()
            local hadTask = resumeState.teleporting
                or resumeState.lockedTarget ~= nil
                or resumeState.lockedTargetUserId ~= nil
                or resumeState.summonTarget ~= nil
                or resumeState.stomponly
                or resumeState.bringonly
                or resumeState.takeonly
                or resumeState.downonly
                or resumeState.opkill
                or resumeState.flingonly
                or resumeState.killall
                or (#resumeState.ragebottargets > 0)
                or resumeState.skyTarget ~= nil
                or resumeState.savedTarget5 ~= nil
                or resumeState.gotoCFrame ~= nil
                or resumeState.gotoTarget ~= nil
                or resumeState.gotoTargetUserId ~= nil
                or resumeState.pendingGotoTarget ~= nil
                or resumeState.pendingGotoTargetUserId ~= nil

            if hadTask then
                lockedTarget = resumeState.lockedTarget
                lockedTargetUserId = resumeState.lockedTargetUserId
                autoLocked = resumeState.autoLocked
                summonTarget = resumeState.summonTarget
                stomponly = resumeState.stomponly
                bringonly = resumeState.bringonly
                takeonly = resumeState.takeonly
                getgenv().downonly = resumeState.downonly
                opkill = resumeState.opkill
                flingonly = resumeState.flingonly
                killall = resumeState.killall
                ragebottargets = copyListRefs(resumeState.ragebottargets)
                shouldSwitch = resumeState.shouldSwitch
                currentTargetIndex = resumeState.currentTargetIndex
                skyTarget = resumeState.skyTarget
                savedTarget5 = resumeState.savedTarget5
                commandSender = resumeState.commandSender
                gotoCFrame = resumeState.gotoCFrame
                gotoTarget = (resumeState.gotoTargetUserId and Players:GetPlayerByUserId(resumeState.gotoTargetUserId)) or resumeState.gotoTarget
                gotoTargetUserId = resumeState.gotoTargetUserId or (gotoTarget and gotoTarget.UserId) or nil
                pendingGotoTarget = (resumeState.pendingGotoTargetUserId and Players:GetPlayerByUserId(resumeState.pendingGotoTargetUserId)) or resumeState.pendingGotoTarget
                pendingGotoTargetUserId = resumeState.pendingGotoTargetUserId or (pendingGotoTarget and pendingGotoTarget.UserId) or nil
                forceBringDrop = resumeState.forceBringDrop
                teleporting = resumeState.teleporting
                if teleporting then
                    voiding = false
                else
                    voiding = resumeState.voiding
                end
            else
                commandSender = nil
                gotoCFrame = nil
                gotoTarget = nil
                gotoTargetUserId = nil
                pendingGotoTarget = nil
                pendingGotoTargetUserId = nil
                forceBringDrop = false
                teleporting = false
                if not resumeOwnerFollow() then
                    voiding = true
                end
            end
        end
        local restoredAfterAutosave = false
        local function restoreAfterAutosaveOnce()
            if restoredAfterAutosave then
                return
            end
            restoredAfterAutosave = true
            restoreAfterAutosave()
        end

        lastSaveAt = os.clock()
        savingActive = true
        autosaveActive = true

        -- pause other behaviors
        lockedTarget = nil
        lockedTargetUserId = nil
        autoLocked = false
        teleporting = false
        voiding = false
        summonTarget = nil
        stomponly = false
        bringonly = false
        takeonly = false
        getgenv().downonly = false
        opkill = false
        flingonly = false
        killall = false
        ragebottargets = {}
        shouldSwitch = false
        skyTarget = nil
        savedTarget5 = nil
        commandSender = nil
        gotoCFrame = nil
        gotoTarget = nil
        gotoTargetUserId = nil
        pendingGotoTarget = nil
        pendingGotoTargetUserId = nil
        forceBringDrop = false

        withNoclip(function()
            local released = false
            local autosaveCompleted = false
            local function confirmAutosaveGrab()
                return isHoldingTargetForDelivery(ownerChar)
            end

            local grabbed = attemptReliableBringGrab(ownerChar, confirmAutosaveGrab, AUTOSAVE_GRAB_ROUNDS, {
                approachOffsets = AUTOSAVE_GRAB_APPROACH_OFFSETS,
                settleTime = 0.04,
                recheckWait = 0.08,
                targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
            })
            if not grabbed then
                local autosaveLockParts = getGrabTargetParts(ownerChar, DELIVERY_OWNER_GRAB_PART_NAMES)
                local autosaveLockPart = autosaveLockParts[1] or ownerPart
                if autosaveLockPart and autosaveLockPart.Parent then
                    local lockOffset = AUTOSAVE_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 2.0, 0)
                    local lockPos = autosaveLockPart.Position + lockOffset
                    moveStandToCFrameExact(myChar, myHRP, CFrame.lookAt(lockPos, autosaveLockPart.Position))
                    task.wait(0.03)
                end
                grabbed = attemptReliableBringGrab(ownerChar, confirmAutosaveGrab, AUTOSAVE_GRAB_HARDLOCK_ROUNDS, {
                    approachOffsets = AUTOSAVE_GRAB_HARDLOCK_OFFSETS,
                    settleTime = 0.05,
                    recheckWait = 0.1,
                    targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                })
            end
            if grabbed and not ensureCarryAttachedToStand(ownerChar, AUTOSAVE_ATTACH_CONFIRM_LOOPS, AUTOSAVE_ATTACH_CONFIRM_WAIT, AUTOSAVE_ATTACH_CONFIRM_DISTANCE) then
                grabbed = false
                logDrop("autosave grab is not attached to stand yet; retrying")
                local autosaveLockParts = getGrabTargetParts(ownerChar, DELIVERY_OWNER_GRAB_PART_NAMES)
                local autosaveLockPart = autosaveLockParts[1] or ownerPart
                if autosaveLockPart and autosaveLockPart.Parent then
                    local lockOffset = AUTOSAVE_GRAB_HARDLOCK_OFFSETS[1] or Vector3.new(0, 2.0, 0)
                    local lockPos = autosaveLockPart.Position + lockOffset
                    moveStandToCFrameExact(myChar, myHRP, CFrame.lookAt(lockPos, autosaveLockPart.Position))
                    task.wait(0.03)
                end
                grabbed = attemptReliableBringGrab(ownerChar, confirmAutosaveGrab, AUTOSAVE_GRAB_HARDLOCK_ROUNDS, {
                    approachOffsets = AUTOSAVE_GRAB_HARDLOCK_OFFSETS,
                    settleTime = 0.05,
                    recheckWait = 0.1,
                    targetPartNames = DELIVERY_OWNER_GRAB_PART_NAMES,
                })
                if grabbed and not ensureCarryAttachedToStand(ownerChar, AUTOSAVE_ATTACH_CONFIRM_LOOPS, AUTOSAVE_ATTACH_CONFIRM_WAIT, AUTOSAVE_ATTACH_CONFIRM_DISTANCE) then
                    grabbed = false
                    logDrop("autosave grab still not attached after hardlock retry")
                end
            end
            if grabbed then
                autosaveFailures = 0

                local ownerHum = ownerChar and ownerChar:FindFirstChildOfClass("Humanoid")
                local ownerHRP = ownerChar and ownerChar:FindFirstChild("HumanoidRootPart")
                local ownerSafePos = autoSavePosition
                local standReleasePos = ownerSafePos + Vector3.new(0, AUTOSAVE_SETTLE_HEIGHT, 0)
                local hoverCFrame = CFrame.new(standReleasePos + Vector3.new(0, AUTOSAVE_HOVER_HEIGHT, 0))
                local settleCFrame = CFrame.new(standReleasePos)
                local ownerNearSafe = false
                local myCharNow = LocalPlayer.Character
                local myHRPNow = myCharNow and myCharNow:FindFirstChild("HumanoidRootPart")
                local function pinOwnerToSafeSpot(loopCount, requireGrab)
                    if not ownerRoot then
                        return ownerHRP == nil
                    end
                    local loops = math.max(loopCount or AUTOSAVE_OWNER_PIN_LOOPS, 1)
                    local pinned = false
                    for _ = 1, loops do
                        if requireGrab and not confirmAutosaveGrab() then
                            break
                        end
                        ownerRoot.CFrame = CFrame.new(ownerSafePos)
                        resetPartVelocity(ownerRoot)
                        if ownerHRP and ownerHRP ~= ownerRoot then
                            ownerHRP.CFrame = CFrame.new(ownerSafePos)
                            resetPartVelocity(ownerHRP)
                        end
                        if myHRPNow then
                            moveStandToCFrameExact(myCharNow, myHRPNow, settleCFrame)
                            resetPartVelocity(myHRPNow)
                        end
                        pinned = isNearPosition(ownerRoot, ownerSafePos, AUTOSAVE_OWNER_PIN_DISTANCE)
                        if pinned then
                            break
                        end
                        task.wait(AUTOSAVE_OWNER_PIN_WAIT)
                    end
                    return pinned or isNearPosition(ownerRoot, ownerSafePos, AUTOSAVE_OWNER_PIN_DISTANCE)
                end

                if myHRPNow then
                    resetPartVelocity(myHRPNow)
                    if ownerHum then
                        pcall(function()
                            ownerHum:ChangeState(Enum.HumanoidStateType.Physics)
                        end)
                        ownerHum.PlatformStand = true
                    end
                    if ownerHRP then
                        resetPartVelocity(ownerHRP)
                    end

                    moveStandToCFrameExact(myCharNow, myHRPNow, hoverCFrame)
                    local hoverArrived, ownerHoverArrived = alignCarryDropPosition(
                        myCharNow,
                        myHRPNow,
                        ownerHRP,
                        hoverCFrame,
                        standReleasePos,
                        AUTOSAVE_CARRY_TIMEOUT,
                        AUTOSAVE_STAND_DISTANCE,
                        AUTOSAVE_OWNER_DISTANCE
                    )
                    if not hoverArrived then
                        logDrop("autosave hover carry did not reach safe position")
                    end
                    if ownerHRP and not ownerHoverArrived then
                        logDrop("autosave owner desync while carrying")
                    end

                    clampOwnerAboveTarget(myCharNow, myHRPNow, ownerHRP, ownerSafePos.Y)
                    if ownerHRP then
                        resetPartVelocity(ownerHRP)
                    end

                    local settleArrived, ownerSettleArrived = alignCarryDropPosition(
                        myCharNow,
                        myHRPNow,
                        ownerHRP,
                        settleCFrame,
                        standReleasePos,
                        AUTOSAVE_SETTLE_TIMEOUT,
                        AUTOSAVE_STAND_DISTANCE,
                        AUTOSAVE_OWNER_DISTANCE
                    )
                    if not settleArrived then
                        logDrop("autosave settle did not reach safe position")
                    end
                    if ownerHRP and not ownerSettleArrived then
                        logDrop("autosave owner still not synced at safe position")
                    end

                    local standNearSafe = isNearPosition(myHRPNow, standReleasePos, AUTOSAVE_STAND_DISTANCE)
                    if ownerHRP then
                        for _ = 1, 8 do
                            ownerNearSafe = pinOwnerToSafeSpot(AUTOSAVE_OWNER_PIN_LOOPS, true)
                            standNearSafe = isNearPosition(myHRPNow, standReleasePos, AUTOSAVE_STAND_DISTANCE)
                            if ownerNearSafe and standNearSafe then
                                break
                            end
                            if not confirmAutosaveGrab() then
                                break
                            end
                            moveStandToCFrameExact(myCharNow, myHRPNow, settleCFrame)
                            resetPartVelocity(myHRPNow)
                            resetPartVelocity(ownerHRP)
                            task.wait(0.04)
                        end
                    else
                        ownerNearSafe = true
                    end

                    if ownerNearSafe and standNearSafe and confirmAutosaveGrab() then
                        task.wait(0.04)
                        released = releaseGrab(ownerChar)
                        if not released and ownerRoot then
                            pinOwnerToSafeSpot(AUTOSAVE_OWNER_PIN_LOOPS, true)
                            task.wait(0.05)
                            released = releaseGrab(ownerChar)
                        end
                        if released then
                            ownerNearSafe = pinOwnerToSafeSpot(AUTOSAVE_POST_RELEASE_PIN_LOOPS, false)
                            autosaveCompleted = ownerNearSafe and (not ownerHRP or isNearPosition(ownerHRP, ownerSafePos, AUTOSAVE_RELEASE_DISTANCE + 1))
                        end
                    end

                    if ownerHRP then
                        resetPartVelocity(ownerHRP)
                    end
                    if ownerHum then
                        ownerHum.PlatformStand = false
                        pcall(function()
                            ownerHum:ChangeState(Enum.HumanoidStateType.GettingUp)
                        end)
                    end
                end

                if not autosaveCompleted and ownerRoot then
                    ownerNearSafe = pinOwnerToSafeSpot(AUTOSAVE_POST_RELEASE_PIN_LOOPS, confirmAutosaveGrab())
                    task.wait(0.05)
                    if confirmAutosaveGrab() then
                        released = releaseGrab(ownerChar)
                    end
                    if released then
                        ownerNearSafe = pinOwnerToSafeSpot(AUTOSAVE_POST_RELEASE_PIN_LOOPS, false)
                        autosaveCompleted = ownerNearSafe and isNearPosition(ownerRoot, ownerSafePos, AUTOSAVE_RELEASE_DISTANCE + 1)
                    end
                end

                if not released then
                    voiding = false
                    task.delay(0.45, function()
                        if confirmAutosaveGrab() then
                            return
                        end
                        if not resumeOwnerFollow() then
                            voiding = true
                        end
                    end)
                end
            end

            if autosaveCompleted then
                autosaveFailures = 0
                autosaveCooldownUntil = os.clock() + AUTOSAVE_SUCCESS_COOLDOWN
            else
                autosaveFailures += 1
                if autosaveFailures >= autosaveMaxFailures then
                    autosaveCooldownUntil = os.clock() + AUTOSAVE_HARD_FAIL_COOLDOWN
                    autosaveFailures = 0
                else
                    autosaveCooldownUntil = os.clock() + AUTOSAVE_FAIL_COOLDOWN
                end
            end
        end)

        autosaveActive = false
        if isHoldingTargetForDelivery(ownerChar) then
            voiding = false
            task.delay(0.4, function()
                if autosaveActive then
                    return
                end
                if isHoldingTargetForDelivery(ownerChar) then
                    releaseGrab(ownerChar)
                end
                if not isHoldingTargetForDelivery(ownerChar) then
                    restoreAfterAutosaveOnce()
                end
            end)
        else
            restoreAfterAutosaveOnce()
        end

        -- Cooldown window to stop re-trigger spam while KO remains true
        task.delay(0.45, function()
            savingActive = false
        end)
    end
end)

function getVehicleRootPart(vehicle)
    if not vehicle then
        return nil
    end
    return vehicle.PrimaryPart or vehicle:FindFirstChildWhichIsA("BasePart", true)
end

function findVehicleModel()
    if vehicleModel and vehicleModel.Parent then
        return vehicleModel
    end
    local now = os.clock()
    if now - lastVehicleSearch < 0.75 then
        return vehicleModel
    end
    lastVehicleSearch = now

    local closest = nil
    local closestDist = nil
    for _, obj in ipairs(workspace:GetDescendants()) do
        if obj:IsA("Model") and obj.Name == vehicleName then
            local root = getVehicleRootPart(obj)
            if root then
                local dist = (root.Position - vehicleSeatCFrame.Position).Magnitude
                if not closestDist or dist < closestDist then
                    closest = obj
                    closestDist = dist
                end
            else
                closest = obj
            end
        end
    end

    vehicleModel = closest
    return vehicleModel
end

function getVehicleSeats(vehicle)
    if not vehicle then
        return nil, nil
    end
    local driverSeat = vehicle:FindFirstChild(vehicleSeatName, true)
    local passengerSeat = nil
    for _, seat in ipairs(vehicle:GetDescendants()) do
        if seat:IsA("Seat") and seat.Name == passengerSeatName then
            passengerSeat = seat
            break
        end
    end
    if passengerSeat == driverSeat then
        passengerSeat = nil
    end
    return driverSeat, passengerSeat
end

function moveAssembly(part, targetCFrame)
    if not (part and targetCFrame) then
        return
    end
    part.AssemblyLinearVelocity = Vector3.zero
    part.AssemblyAngularVelocity = Vector3.zero
    part.CFrame = targetCFrame
end

function moveVehicleRootToSeat(rootPart, seatPart, desiredSeatCFrame)
    if not (rootPart and seatPart and desiredSeatCFrame) then
        return
    end
    local seatOffset = rootPart.CFrame:ToObjectSpace(seatPart.CFrame)
    local targetRoot = desiredSeatCFrame * seatOffset:Inverse()
    moveAssembly(rootPart, targetRoot)
end

function getVehicleDestinationCFrame()
    if gotoTarget then
        local targetChar = gotoTarget.Character
        local targetHRP = targetChar and targetChar:FindFirstChild("HumanoidRootPart")
        if targetHRP then
            return CFrame.new(targetHRP.Position)
        end
        return nil
    end
    return gotoCFrame
end

function tryPurchaseVehicle()
    if not vehiclePurchaseEnabled then
        return false
    end
    if buyingVehicleInProgress then
        return false
    end
    if buyingGunInProgress or buyingMaskInProgress or buyingArmorInProgress then
        return false
    end
    local now = os.clock()
    if now - lastVehiclePurchase < 1 then
        return false
    end

    local char = LocalPlayer.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    local humanoid = char and char:FindFirstChildOfClass("Humanoid")
    if not (root and humanoid and humanoid.Health > 0) then
        return false
    end

    local shopFolder = workspace:FindFirstChild("Ignored") and workspace.Ignored:FindFirstChild("Shop")
    local cartItem = shopFolder and findShopItem(shopFolder, vehicleShopName, {ammo = false})
    local clickDetector = cartItem and cartItem:FindFirstChildWhichIsA("ClickDetector", true)
    local shopBase = getShopBasePart(cartItem, clickDetector)
    if not clickDetector or not shopBase then
        return false
    end

    local prevBuying = buyingInProgress
    buyingVehicleInProgress = true
    buyingInProgress = true

    withNoclip(function()
        safeTeleportToShop(root, shopBase)
        getgenv().fireclickdetector(clickDetector)
        task.wait(0.2)
    end)

    buyingInProgress = prevBuying
    buyingVehicleInProgress = false
    requestIdleVoidReturn(0.06)
    lastVehiclePurchase = os.clock()
    return true
end

-- Vehicle Mode Handler
task.spawn(function()
    while task.wait(0.1) do
        if vehicleMode and gotoPlayer and (gotoCFrame or gotoTarget) then
            local lp = LocalPlayer
            local char = lp.Character
            if not char then continue end

            local hrp = char:FindFirstChild("HumanoidRootPart")
            local humanoid = char:FindFirstChildOfClass("Humanoid")
            local ownerChar = gotoPlayer.Character
            local ownerHRP = ownerChar and ownerChar:FindFirstChild("HumanoidRootPart")
            if not (hrp and humanoid and ownerHRP) then continue end

            local destCFrame = getVehicleDestinationCFrame()
            if not destCFrame then continue end

            local vehicle = findVehicleModel()
            if not vehicle then
                local distToPickup = (hrp.Position - vehiclePickupPos).Magnitude
                if distToPickup > 4 then
                    moveAssembly(hrp, CFrame.new(vehiclePickupPos + Vector3.new(0, 3, 0)))
                else
                    tryPurchaseVehicle()
                end
                continue
            end

            local driverSeat, passengerSeat = getVehicleSeats(vehicle)
            local vehicleRoot = driverSeat or getVehicleRootPart(vehicle) or hrp

            if driverSeat then
                if driverSeat.Occupant and driverSeat.Occupant ~= humanoid then
                    continue
                end
                if humanoid.SeatPart ~= driverSeat then
                    moveAssembly(vehicleRoot, vehicleSeatCFrame)
                    task.wait(0.05)
                    pcall(function()
                        driverSeat:Sit(humanoid)
                    end)
                    continue
                end
            else
                moveAssembly(hrp, vehicleSeatCFrame)
                continue
            end

            local ownerHumanoid = ownerChar and ownerChar:FindFirstChildOfClass("Humanoid")
            if passengerSeat and ownerHumanoid then
                if passengerSeat.Occupant ~= ownerHumanoid then
                    if passengerSeat.Occupant and passengerSeat.Occupant ~= ownerHumanoid then
                        continue
                    end
                    local desiredSeatCFrame = ownerHRP.CFrame * CFrame.new(0, 0, 1.5)
                    moveVehicleRootToSeat(vehicleRoot, passengerSeat, desiredSeatCFrame)
                    continue
                end
            else
                local behindOwner = ownerHRP.CFrame * CFrame.new(0, 0, 5)
                moveAssembly(vehicleRoot, behindOwner)
            end

            local distToDest = (vehicleRoot.Position - destCFrame.Position).Magnitude
            if distToDest > 3 then
                moveAssembly(vehicleRoot, destCFrame)
            else
                vehicleMode = false
                gotoPlayer = nil
                gotoCFrame = nil
                gotoTarget = nil
                vehicleModel = nil
                voiding = true
            end
        end
    end
end)

hitboxsize = LowLagMode and 12 or 30
lastHitboxUpdate = 0

function restorePerformanceDefaults()
    if not defaultConfigCaptured then
        captureDefaultConfig()
    end

    LowLagMode = defaultConfig.LowLagMode
    for k, v in pairs(defaultPerf) do
        perf[k] = v
    end
    restoreDefaultCombatConfig()
    applyDefaultScalarConfig()

    shootInterval = perf.shoot
    pcall(function()
        setfpscap(FPSCap)
    end)
end

deactivateStandPerformanceMode = function(silent)
    if not standPerformanceModeActive then
        if not silent then
            sendMessage("Stand performance mode is already disabled.")
        end
        return
    end

    restorePerformanceDefaults()
    standPerformanceModeActive = false

    if not silent then
        sendMessage("Stand performance mode disabled.")
    end
end

activateStandPerformanceMode = function(forceOn)
    if standPerformanceModeActive then
        if forceOn then
            sendMessage("Stand performance mode is already enabled.")
        else
            deactivateStandPerformanceMode()
        end
        return
    end

    captureDefaultConfig()
    if powerModeActive and deactivatePowerMode then
        deactivatePowerMode(true)
    end

    standPerformanceModeActive = true
    LowLagMode = false

    -- Stand-first profile: faster follow updates with safer burst limits.
    perf.loop = 0.02
    perf.combat = 0.02
    perf.void = 0.08
    perf.teleport = 0.0075
    perf.teleportCombat = 0.0063
    perf.target = 0.04
    perf.summon = 0.04
    perf.mask = 0.08
    perf.equip = 0.06
    perf.killall = 0.08
    perf.hitbox = 0.3
    perf.shoot = 0.02

    combatConfig.maxRange = 420
    combatConfig.sightRangeMultiplier = 2.1
    combatConfig.bulletSpeed = 680
    combatConfig.leadTimeMin = 0.1
    combatConfig.leadTimeMax = 1.1
    combatConfig.leadScale = 1.05
    combatConfig.standDuelTargetSpeedThreshold = 56
    combatConfig.standDuelExtremeSpeedThreshold = 128
    combatConfig.standDuelVelocitySample = 1850
    combatConfig.standDuelVelocityBlend = 0.9
    combatConfig.standDuelVelocitySmoothing = 0.978
    combatConfig.standDuelExtremeVelocitySmoothing = 0.995
    combatConfig.standDuelPredictionBoost = 0.5
    combatConfig.standDuelExtremePredictionBoost = 0.76
    combatConfig.standDuelFollowSpeedBoost = 3.0
    combatConfig.standDuelExtremeFollowSpeedBoost = 1.92
    combatConfig.standDuelSpeedCap = 690
    combatConfig.standDuelExtremeSpeedCap = 860
    combatConfig.standDuelSnapDistance = 42
    combatConfig.standDuelFollowMinDelay = 0.00082
    combatConfig.standDuelLoopOrbitSpeedBoost = 1.58
    combatConfig.standDuelLoopLeadTimeBoost = 0.54
    combatConfig.standDuelLoopLeadScaleBoost = 0.4
    combatConfig.standDuelAttackLeadTimeBoost = 0.22
    combatConfig.standDuelAttackLeadScaleBoost = 0.16
    combatConfig.attackPreferredRange = 108
    combatConfig.attackMaxRange = 520
    combatConfig.attackShootRange = 3900
    combatConfig.attackBlindShootRange = 5600
    combatConfig.attackSightRangeMultiplier = 7.8
    combatConfig.attackShootInterval = 0.0023
    combatConfig.attackMinShootInterval = 0.0017
    combatConfig.attackShotsPerTick = 9
    combatConfig.attackLeadTimeMax = 1.9
    combatConfig.attackLeadScale = 2.25
    combatConfig.attackPredictionBoost = 0.2
    combatConfig.attackFollowSpeedBoost = 1.52
    combatConfig.attackExtremeFollowSpeedBoost = 1.38
    combatConfig.attackCircleRadius = 12.4
    combatConfig.attackCircleStrafeSpeed = 600
    combatConfig.attackCircleHeight = 4.9
    combatConfig.attackCircleHeightBob = 0.12
    combatConfig.attackFollowMinDelay = 0.00125
    combatConfig.indoorCheckInterval = 0.2
    combatConfig.indoorShootInterval = 0.008
    combatConfig.indoorShotsPerTick = 20
    combatConfig.loopShootRange = 14000
    combatConfig.loopBlindShootRange = 21000
    combatConfig.loopSightRangeMultiplier = 9.2
    combatConfig.loopShootInterval = 0.0034
    combatConfig.loopMinShootInterval = 0.0024
    combatConfig.loopShotsPerTick = 10
    combatConfig.loopLeadTimeMax = 6.45
    combatConfig.loopLeadScale = 3.32
    combatConfig.loopMinRange = 240
    combatConfig.loopPreferredRange = 330
    combatConfig.loopMaxRange = 520
    combatConfig.loopFollowMinDelay = 0.00096
    combatConfig.loopOrbitRadius = 64
    combatConfig.loopOrbitSpeed = 194
    combatConfig.loopSkyStrafeSpeed = 700
    combatConfig.loopSkyStrafeRadiusPull = 0.24
    combatConfig.loopSkyStrafeHeightBob = 1.1
    combatConfig.indoorOrbitRadius = 11
    combatConfig.indoorOrbitSpeed = 176
    combatConfig.indoorCircleRadius = 13
    combatConfig.indoorCircleStrafeSpeed = 360
    combatConfig.indoorCircleHeight = 4.8
    combatConfig.sentryCircleRadius = 9.6
    combatConfig.sentryCircleStrafeSpeed = 500
    combatConfig.sentryCircleHeight = 4.2
    combatConfig.sentryCircleHeightBob = 0.16
    combatConfig.sentryShootInterval = 0.0034
    combatConfig.sentryMinShootInterval = 0.0023
    combatConfig.sentryShotsPerTick = 10
    combatConfig.sentryFollowMinDelay = 0.00125

    auraspeed = 20
    auradistance = 4
    homeFollowDistance = 5.2
    homeFollowSideOffset = 2.5
    homeFollowHeight = 1.2
    homeFollowPredictionTime = 0.1255
    homeFollowCatchup = 0.82
    homeFollowSnapDistance = 36
    homeFollowFarSnapDistance = 84
    homeFollowMotionSpeed = 6.8
    homeFollowSideWave = 0.82
    homeFollowBob = 0.1
    homeFollowMaxDistanceBoost = 3.1
    homeFollowLookHeight = 1.4
    shotsPerTick = 6
    followShotsPerTick = 3
    followShotCooldown = 0.035
    followGridCellSize = 8
    followGridRadius = 220
    followMaxTargets = 12
    reloadCooldown = 0.3
    hitboxsize = 14
    FPSCap = 90
    ArmorRecheckDelay = 1.5
    shootInterval = perf.shoot

    auraangle = math.random() * math.pi * 2
    pcall(function()
        setfpscap(FPSCap)
    end)

    if getgenv().enabled and standHomeName then
        startFollowingTarget(standHomeName)
    end

    sendMessage("Stand performance mode enabled: smooth, fast, low lag.")
end

deactivatePowerMode = function(silent)
    if not powerModeActive then
        return
    end

    restorePerformanceDefaults()
    powerModeActive = false

    -- Reset any combat/loop state that can hijack follow/smoothness after POWER MODE.
    ragebottargets = {}
    shouldSwitch = false
    lockedTarget = nil
    lockedTargetUserId = nil
    teleporting = false

    -- If owner follow is enabled, rebind and keep stand out of void.
    if getgenv().enabled and standHomeName then
        startFollowingTarget(standHomeName)
        voiding = false
    end

    if not silent then
        sendMessage("POWER MODE disabled.")
    end
end

activatePowerMode = function()
    if powerModeActive then
        deactivatePowerMode()
        return
    end
    captureDefaultConfig()
    if standPerformanceModeActive and deactivateStandPerformanceMode then
        deactivateStandPerformanceMode(true)
    end
    powerModeActive = true

    -- POWER MODE: ultra-aggressive chase/prediction with a still-safe remote budget.
    LowLagMode = false
    restoreDefaultCombatConfig()

    perf.loop = 0.01
    perf.combat = 0.009
    perf.void = 0.04
    perf.teleport = 0.0046
    perf.teleportCombat = 0.0039
    perf.target = 0.018
    perf.summon = 0.018
    perf.mask = 0.04
    perf.equip = 0.025
    perf.killall = 0.04
    perf.hitbox = 0.08
    perf.shoot = 0.009

    combatConfig.maxRange = 560
    combatConfig.sightRangeMultiplier = 2.45
    combatConfig.bulletSpeed = 780
    combatConfig.leadTimeMin = 0.09
    combatConfig.leadTimeMax = 1.28
    combatConfig.leadScale = 1.2
    combatConfig.velocityBlend = 0.62
    combatConfig.fastVelocitySmoothing = 0.94
    combatConfig.maxVelocitySample = 980
    combatConfig.fastTargetPredictionBoost = 0.72
    combatConfig.extremeTargetPredictionBoost = 0.98
    combatConfig.fastTargetFollowSpeedBoost = 2.82
    combatConfig.extremeTargetFollowSpeedBoost = 1.72
    combatConfig.standDuelTargetSpeedThreshold = 52
    combatConfig.standDuelExtremeSpeedThreshold = 120
    combatConfig.standDuelVelocitySample = 2100
    combatConfig.standDuelVelocityBlend = 0.92
    combatConfig.standDuelVelocitySmoothing = 0.985
    combatConfig.standDuelExtremeVelocitySmoothing = 0.997
    combatConfig.standDuelPredictionBoost = 0.7
    combatConfig.standDuelExtremePredictionBoost = 1.02
    combatConfig.standDuelFollowSpeedBoost = 3.82
    combatConfig.standDuelExtremeFollowSpeedBoost = 2.34
    combatConfig.standDuelSpeedCap = 920
    combatConfig.standDuelExtremeSpeedCap = 1080
    combatConfig.standDuelSnapDistance = 52
    combatConfig.standDuelFollowMinDelay = 0.00062
    combatConfig.standDuelLoopOrbitSpeedBoost = 1.6
    combatConfig.standDuelLoopLeadTimeBoost = 0.58
    combatConfig.standDuelLoopLeadScaleBoost = 0.42
    combatConfig.standDuelAttackLeadTimeBoost = 0.24
    combatConfig.standDuelAttackLeadScaleBoost = 0.18
    combatConfig.attackPreferredRange = 112
    combatConfig.attackMaxRange = 640
    combatConfig.attackShootRange = 4600
    combatConfig.attackBlindShootRange = 6600
    combatConfig.attackSightRangeMultiplier = 8.2
    combatConfig.attackShootInterval = 0.0019
    combatConfig.attackMinShootInterval = 0.0014
    combatConfig.attackShotsPerTick = 10
    combatConfig.attackLeadTimeMax = 1.95
    combatConfig.attackLeadScale = 2.34
    combatConfig.attackPredictionBoost = 0.32
    combatConfig.attackFollowSpeedBoost = 1.86
    combatConfig.attackExtremeFollowSpeedBoost = 1.66
    combatConfig.attackCircleRadius = 10.9
    combatConfig.attackCircleStrafeSpeed = 690
    combatConfig.attackCircleHeight = 4.8
    combatConfig.attackCircleHeightBob = 0.1
    combatConfig.attackFollowMinDelay = 0.0012
    combatConfig.loopShootRange = 22000
    combatConfig.loopBlindShootRange = 29000
    combatConfig.loopSightRangeMultiplier = 11.4
    combatConfig.loopShootInterval = 0.0028
    combatConfig.loopMinShootInterval = 0.002
    combatConfig.loopShotsPerTick = 10
    combatConfig.loopLeadTimeMax = 6.5
    combatConfig.loopLeadScale = 3.62
    combatConfig.loopFollowMinDelay = 0.0009
    combatConfig.loopOrbitRadius = 58
    combatConfig.loopOrbitSpeed = 236
    combatConfig.loopSkyStrafeSpeed = 920
    combatConfig.loopSkyStrafeRadiusPull = 0.25
    combatConfig.loopSkyStrafeHeightBob = 1.15
    combatConfig.indoorShootInterval = 0.0062
    combatConfig.indoorShotsPerTick = 16
    combatConfig.indoorOrbitRadius = 9.8
    combatConfig.indoorOrbitSpeed = 192
    combatConfig.indoorCircleRadius = 12.8
    combatConfig.indoorCircleStrafeSpeed = 370
    combatConfig.indoorCircleHeight = 4.9
    combatConfig.sentryCircleRadius = 8.6
    combatConfig.sentryCircleStrafeSpeed = 710
    combatConfig.sentryCircleHeight = 4.6
    combatConfig.sentryCircleHeightBob = 0.18
    combatConfig.sentryShootInterval = 0.0027
    combatConfig.sentryMinShootInterval = 0.002
    combatConfig.sentryShotsPerTick = 10
    combatConfig.sentryFollowMinDelay = 0.00092

    auraspeed = 34
    auradistance = 4.2
    homeFollowDistance = 5.35
    homeFollowSideOffset = 2.7
    homeFollowHeight = 1.2
    homeFollowPredictionTime = 0.12
    homeFollowCatchup = 0.98
    homeFollowSnapDistance = 40
    homeFollowFarSnapDistance = 90
    homeFollowMotionSpeed = 9.8
    homeFollowSideWave = 0.88
    homeFollowBob = 0.08
    homeFollowMaxDistanceBoost = 3.6
    homeFollowLookHeight = 1.42

    shotsPerTick = 10
    followShotsPerTick = 5
    followShotCooldown = 0.022
    followGunSpacing = 0.012
    followGridCellSize = 7
    followGridRadius = 320
    followMaxTargets = 12
    reloadCooldown = 0.22
    hitboxsize = 24
    FPSCap = 120
    ArmorRecheckDelay = 0.95
    shootInterval = perf.shoot

    auraangle = math.random() * math.pi * 2
    pcall(function()
        setfpscap(FPSCap)
    end)

    if getgenv().enabled and standHomeName then
        startFollowingTarget(standHomeName)
    end
    sendMessage("POWER MODE enabled: longer range, harder chase, and more aggressive tracking with the same network guardrails.")
end

Players = cloneref(game:GetService("Players"))
Client = Players.LocalPlayer

RunService.RenderStepped:Connect(function ()
    if perf.hitbox > 0 then
        local now = os.clock()
        if (now - lastHitboxUpdate) < perf.hitbox then
            return
        end
        lastHitboxUpdate = now
    end
    for _, Player in pairs(Players:GetPlayers()) do
        if Player ~= Client then
            local character = Player.Character
            if character then
                local HRP = character:FindFirstChild("HumanoidRootPart")
                if HRP then
                    HRP.Size = Vector3.new(hitboxsize, hitboxsize, hitboxsize)
                    HRP.CanCollide = false
                end
            end
        end
    end
end)

RunService.Heartbeat:Connect(function()
    if not (flingonly and lockedTarget) then return end

    Player.Character.HumanoidRootPart.Velocity = Vector3.new(99999999, 99999999, 99999999)
    RunService.RenderStepped:Wait()
    Player.Character.HumanoidRootPart.Velocity = Vector3.new(0, 0, 0)
end)

Player.CharacterAdded:Connect(function(newChar)
    Character = newChar
    humanoid = Character:WaitForChild("Humanoid")
    bodyEffects = Character:WaitForChild("BodyEffects")
    koValue = bodyEffects:WaitForChild("K.O")
end)

Workspace = game:GetService("Workspace")

for _, v in ipairs(Workspace:GetDescendants()) do
    if v:IsA("Seat") then
        v:Destroy()
    end
end

Workspace.DescendantAdded:Connect(function(descendant)
    task.defer(function()
        if descendant:IsA("Seat") then
            descendant:Destroy()
        end
    end)
end)

antiConnections = {}

function stripAnimations(character)
    if character:GetAttribute("AntiServerLaggerHandled") then return end
    character:SetAttribute("AntiServerLaggerHandled", true)

    local humanoid = character:WaitForChild("Humanoid", 5)
    if not humanoid then return end

    local animator = humanoid:FindFirstChildOfClass("Animator")
    if animator then
        animator:Destroy()
    end

    local animate = character:FindFirstChild("Animate")
    if animate then
        animate.Disabled = true
    end

    humanoid.AutoRotate = false
end

function onPlayer(player)
    if player == LocalPlayer then return end

    if player.Character then
        stripAnimations(player.Character)
    end

    local charConn = player.CharacterAdded:Connect(stripAnimations)
    table.insert(antiConnections, charConn)
end

function EnableAntiServerLagger()
    for _, player in ipairs(Players:GetPlayers()) do
        onPlayer(player)
    end

    antiConnections.playerAdded = Players.PlayerAdded:Connect(onPlayer)
end

EnableAntiServerLagger()

if BlackScreen then
    pcall(function()
        local Players = game:GetService("Players")
        local player = Players.LocalPlayer
        local cam = workspace.CurrentCamera

        cam.CameraType = Enum.CameraType.Scriptable
        cam.CFrame = CFrame.new(99999, 99999, 99999)

        player.CharacterAdded:Connect(function()
            task.wait(1)
            cam.CameraType = Enum.CameraType.Scriptable
            cam.CFrame = CFrame.new(99999, 99999, 99999)
        end)

        workspace.Terrain:Clear()

        for _, obj in pairs(workspace:GetDescendants()) do
            if obj:IsA("Decal") or obj:IsA("Texture") or obj:IsA("ParticleEmitter") or obj:IsA("Light") then
                obj:Destroy()
            end
            if obj:IsA("BasePart") then
                obj.Transparency = 1
                obj.CastShadow = false
                obj.Material = Enum.Material.SmoothPlastic
                if obj:FindFirstChild("SurfaceAppearance") then
                    obj.SurfaceAppearance:Destroy()
                end
            end
        end

        local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
        gui.Name = "FPS_BLACKOUT"
        gui.Parent = game.CoreGui
        gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

        local frame = Instance.new("Frame", gui)
        frame.BackgroundColor3 = Color3.new(0, 0, 0)
        frame.Position = UDim2.new(-0.5, 0, -0.5, 0)
        frame.Size = UDim2.new(2, 0, 2, 0)
        frame.ZIndex = 9999
    end)
end

setfpscap(FPSCap)

pcall(function()
    settings().Rendering.QualityLevel = "Level01"
    UserSettings():GetService("UserGameSettings").MasterVolume = 0
end)
pcall(function()
    local lasers = workspace:FindFirstChild("MAP") and workspace.MAP:FindFirstChild("Indestructible") and workspace.MAP.Indestructible:FindFirstChild("Lasers")
    if lasers then
        lasers:Destroy()
    end
end)
pcall(function()
    pcall(function()
        for _, descendant in ipairs(workspace:GetDescendants()) do
            if descendant:IsA("BasePart") then
                descendant.Material = Enum.Material.Plastic
                descendant.Color = Color3.fromRGB(0, 0, 0)
                descendant.Reflectance = 0
                descendant.CastShadow = false
            end
        end

        workspace.DescendantAdded:Connect(function(part)
            if part:IsA("BasePart") then
                part.Material = Enum.Material.Plastic
                part.Color = Color3.fromRGB(0, 0, 0)
                part.Reflectance = 0
                part.CastShadow = false
            end
        end)
    end)

    pcall(function()
        local VirtualUser = game:GetService("VirtualUser")
        game:GetService("Players").LocalPlayer.Idled:Connect(function()
            VirtualUser:CaptureController()
            VirtualUser:ClickButton2(Vector2.new())
        end)
    end)
end)

local function applyAutoBalancedDefaults()
    LowLagMode = true

    perf.loop = 0.03
    perf.combat = 0.018
    perf.void = 0.14
    perf.teleport = 0.016
    perf.teleportCombat = 0.0066
    perf.target = 0.045
    perf.summon = 0.045
    perf.mask = 0.1
    perf.equip = 0.1
    perf.killall = 0.1
    perf.hitbox = 0.3
    perf.shoot = 0.02

    combatConfig.maxRange = 360
    combatConfig.sightRangeMultiplier = 1.85
    combatConfig.bulletSpeed = 610
    combatConfig.leadTimeMin = 0.11
    combatConfig.leadTimeMax = 1.06
    combatConfig.leadScale = 1.02
    combatConfig.standDuelTargetSpeedThreshold = 48
    combatConfig.standDuelExtremeSpeedThreshold = 108
    combatConfig.standDuelVelocitySample = 1400
    combatConfig.standDuelVelocityBlend = 0.82
    combatConfig.standDuelVelocitySmoothing = 0.95
    combatConfig.standDuelExtremeVelocitySmoothing = 0.985
    combatConfig.standDuelPredictionBoost = 0.42
    combatConfig.standDuelExtremePredictionBoost = 0.64
    combatConfig.standDuelFollowSpeedBoost = 2.85
    combatConfig.standDuelExtremeFollowSpeedBoost = 1.72
    combatConfig.standDuelSpeedCap = 560
    combatConfig.standDuelExtremeSpeedCap = 720
    combatConfig.standDuelSnapDistance = 38
    combatConfig.standDuelFollowMinDelay = 0.00125
    combatConfig.standDuelLoopOrbitSpeedBoost = 1.34
    combatConfig.standDuelLoopLeadTimeBoost = 0.35
    combatConfig.standDuelLoopLeadScaleBoost = 0.24
    combatConfig.standDuelAttackLeadTimeBoost = 0.16
    combatConfig.standDuelAttackLeadScaleBoost = 0.12
    combatConfig.attackPreferredRange = 88
    combatConfig.attackMaxRange = 380
    combatConfig.attackShootRange = 2800
    combatConfig.attackBlindShootRange = 3800
    combatConfig.attackSightRangeMultiplier = 5.8
    combatConfig.attackShootInterval = 0.0036
    combatConfig.attackMinShootInterval = 0.0026
    combatConfig.attackShotsPerTick = 8
    combatConfig.attackLeadTimeMax = 1.35
    combatConfig.attackLeadScale = 1.65
    combatConfig.attackPredictionBoost = 0.19
    combatConfig.attackFollowSpeedBoost = 1.55
    combatConfig.attackExtremeFollowSpeedBoost = 1.34
    combatConfig.attackCircleRadius = 10.8
    combatConfig.attackCircleStrafeSpeed = 560
    combatConfig.attackCircleHeight = 4.4
    combatConfig.attackCircleHeightBob = 0.08
    combatConfig.attackFollowMinDelay = 0.00135
    combatConfig.loopShootRange = 13000
    combatConfig.loopBlindShootRange = 19000
    combatConfig.loopSightRangeMultiplier = 8.8
    combatConfig.loopShootInterval = 0.0039
    combatConfig.loopMinShootInterval = 0.0027
    combatConfig.loopShotsPerTick = 9
    combatConfig.indoorShootInterval = 0.009
    combatConfig.indoorShotsPerTick = 18
    combatConfig.loopLeadTimeMax = 6.2
    combatConfig.loopLeadScale = 3.08
    combatConfig.loopMinRange = 240
    combatConfig.loopPreferredRange = 330
    combatConfig.loopMaxRange = 520
    combatConfig.loopFollowMinDelay = 0.001
    combatConfig.fastTargetFollowSpeedBoost = 2.36
    combatConfig.extremeTargetFollowSpeedBoost = 1.58
    combatConfig.maxVelocitySample = 620
    combatConfig.loopOrbitRadius = 66
    combatConfig.loopOrbitSpeed = 188
    combatConfig.loopSkyStrafeSpeed = 680
    combatConfig.loopSkyStrafeRadiusPull = 0.22
    combatConfig.loopSkyStrafeHeightBob = 1.0
    combatConfig.indoorOrbitRadius = 11
    combatConfig.indoorOrbitSpeed = 180
    combatConfig.indoorCircleRadius = 13.5
    combatConfig.indoorCircleStrafeSpeed = 380
    combatConfig.indoorCircleHeight = 4.6
    combatConfig.sentryCircleRadius = 9.5
    combatConfig.sentryCircleStrafeSpeed = 520
    combatConfig.sentryCircleHeight = 4.2
    combatConfig.sentryCircleHeightBob = 0.16
    combatConfig.sentryShootInterval = 0.0034
    combatConfig.sentryMinShootInterval = 0.0023
    combatConfig.sentryShotsPerTick = 10
    combatConfig.sentryFollowMinDelay = 0.0013

    auraspeed = 11
    auradistance = 3.5
    homeFollowDistance = 4.9
    homeFollowSideOffset = 2.15
    homeFollowHeight = 1.1
    homeFollowPredictionTime = 0.125
    homeFollowCatchup = 0.82
    homeFollowSnapDistance = 38
    homeFollowFarSnapDistance = 88
    homeFollowMotionSpeed = 7.0
    homeFollowSideWave = 0.62
    homeFollowBob = 0.08
    homeFollowMaxDistanceBoost = 2.8
    homeFollowLookHeight = 1.3
    voidAuraSpeed = 20
    voidAuraRadius = 120
    voidAuraRadiusJitter = 20
    voidAuraVerticalBob = 7
    voidAuraCenterDrift = 14
    voidAuraRecenterSeconds = 8

    shotsPerTick = 3
    followShotsPerTick = 1
    followShotCooldown = 0.065
    followGunSpacing = 0.015
    followGridCellSize = 8
    followGridRadius = 170
    followMaxTargets = 8
    reloadCooldown = 0.35
    hitboxsize = 12
    ArmorRecheckDelay = 2
    FPSCap = 90
    shootInterval = math.max(perf.shoot, standTuning.minShootInterval or 0.02)

    auraangle = math.random() * math.pi * 2
    pcall(function()
        setfpscap(FPSCap)
    end)
end

task.defer(function()
    applyAutoBalancedDefaults()

    hardStop = false
    -- Keep stand disabled on startup; require explicit ".a on" command.
    getgenv().enabled = false
    getgenv().enabled1 = false
    teleporting = false
    lockedTarget = nil
    summonTarget = nil
    shouldSwitch = false

    local followName = standHomeName or Owner
    local followPlayer = followName and Players:FindFirstChild(followName)
    if not followPlayer and LocalPlayer then
        followName = LocalPlayer.Name
        followPlayer = LocalPlayer
    end

    if followName then
        standHomeName = followName
    end
    targetPlayer = nil
    voiding = true
end)
