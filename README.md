local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local DataStoreService = game:GetService("DataStoreService")

local AddSeedEvent = Instance.new("RemoteEvent")
AddSeedEvent.Name = "AddSeedEvent"
AddSeedEvent.Parent = ReplicatedStorage

local AddPetEvent = Instance.new("RemoteEvent")
AddPetEvent.Name = "AddPetEvent"
AddPetEvent.Parent = ReplicatedStorage

local InventoryStore = DataStoreService:GetDataStore("InventoryData")
local PetStore = DataStoreService:GetDataStore("PetData")

local function loadPlayerData(player)
	local userId = player.UserId
	local inventory = InventoryStore:GetAsync(userId) or {}
	local pets = PetStore:GetAsync(userId) or {}
	player:SetAttribute("Inventory", HttpService:JSONEncode(inventory))
	player:SetAttribute("Pets", HttpService:JSONEncode(pets))
end

local function savePlayerData(player)
	local userId = player.UserId
	local inventory = player:GetAttribute("Inventory")
	local pets = player:GetAttribute("Pets")
	if inventory then
		InventoryStore:SetAsync(userId, HttpService:JSONDecode(inventory))
	end
	if pets then
		PetStore:SetAsync(userId, HttpService:JSONDecode(pets))
	end
end

Players.PlayerAdded:Connect(loadPlayerData)
Players.PlayerRemoving:Connect(savePlayerData)

AddSeedEvent.OnServerEvent:Connect(function(player, seedName, amount)
	local data = HttpService:JSONDecode(player:GetAttribute("Inventory") or "{}")
	data[seedName] = (data[seedName] or 0) + amount
	player:SetAttribute("Inventory", HttpService:JSONEncode(data))
end)

AddPetEvent.OnServerEvent:Connect(function(player, petName, amount)
	local data = HttpService:JSONDecode(player:GetAttribute("Pets") or "{}")
	data[petName] = (data[petName] or 0) + amount
	player:SetAttribute("Pets", HttpService:JSONEncode(data))
end)

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local AddSeedEvent = ReplicatedStorage:WaitForChild("AddSeedEvent")
local AddPetEvent = ReplicatedStorage:WaitForChild("AddPetEvent")

script.Parent.MouseButton1Click:Connect(function()
	AddSeedEvent:FireServer("Carrot", 5)
	AddPetEvent:FireServer("LuckyCat", 1)
end)
