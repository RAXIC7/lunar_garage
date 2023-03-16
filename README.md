# lunar_garage
Highly optimized garage system that allows you to add as many garages as you wish! (car, boat, air)

Documentation: https://lunar-scripts.gitbook.io/lunar-scripts/free-scripts/lunar_garage

Discord: https://discord.gg/zDK4CHQ56N

Dependencies: es_extended, ox_lib, esx_vehicleshop


Change this

function SpawnVehicle(props)
local garage = Config.Garages[currentData]
ESX.Game.SpawnVehicle(props.model, garage.SpawnPosition, garage.SpawnPosition.w, function(vehicle)
if DoesEntityExist(vehicle) then
ESX.Game.SetVehicleProperties(vehicle, props)
TaskWarpPedIntoVehicle(PlayerPedId(), vehicle, -1)
TriggerServerEvent('lunar_garage:vehicleTakenOut', props.plate)
end
end)
end

To this

function SpawnVehicle(props)
local garage = Config.Garages[currentData]
if ESX.Game.IsSpawnPointClear(vector3(garage.SpawnPosition), 1.0) then
ESX.Game.SpawnVehicle(props.model, garage.SpawnPosition, garage.SpawnPosition.w, function(vehicle)
if DoesEntityExist(vehicle) then
ESX.Game.SetVehicleProperties(vehicle, props)
TaskWarpPedIntoVehicle(PlayerPedId(), vehicle, -1)
TriggerServerEvent('lunar_garage:vehicleTakenOut', props.plate)
end
end)
else
TriggerEvent(Config.Notify, 'Please move the vehicle blocking spawn point')
end
end
