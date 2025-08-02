local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

local AddSeedEvent = ReplicatedStorage:WaitForChild("AddSeedEvent")
local AddPetEvent = ReplicatedStorage:WaitForChild("AddPetEvent")

local InventoryData = {}
local PetData = {}

local function addSeed(player, seedName, amount)
	local userId = player.UserId
	if not InventoryData[userId] then
		InventoryData[userId] = {}
	end
	InventoryData[userId][seedName] = (InventoryData[userId][seedName] or 0) + amount
end

local function addPet(player, petName, amount)
	local userId = player.UserId
	if not PetData[userId] then
		PetData[userId] = {}
	end
	PetData[userId][petName] = (PetData[userId][petName] or 0) + amount
end

AddSeedEvent.OnServerEvent:Connect(function(player, seedName, amount)
	addSeed(player, seedName, amount)
end)

AddPetEvent.OnServerEvent:Connect(function(player, petName, amount)
	addPet(player, petName, amount)
end)
