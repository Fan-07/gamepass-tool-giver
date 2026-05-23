local MarketplaceService = game:GetService("MarketplaceService")
local Players = game:GetService("Players")
local ServerStorage = game:GetService("ServerStorage")

local GAMEPASS_ID = 1836351062 -- replace with your pass id
local TOOL_NAME = "yourtoolname" --put your actual tool

local function giveTool(player)
	local tool = ServerStorage:FindFirstChild(TOOL_NAME)
	if not tool then return end

	-- Backpack
	if not player.Backpack:FindFirstChild(TOOL_NAME) then
		tool:Clone().Parent = player.Backpack
	end

	-- StarterGear = keep your tool even after death
	if not player:FindFirstChild("StarterGear"):FindFirstChild(TOOL_NAME) then
		tool:Clone().Parent = player.StarterGear
	end
end

Players.PlayerAdded:Connect(function(player)

	local ownsPass = false
	local success, result = pcall(function()
		return MarketplaceService:UserOwnsGamePassAsync(player.UserId, GAMEPASS_ID)
	end)

	if success then
		ownsPass = result
	end

	if ownsPass then
		player.CharacterAdded:Connect(function()
			task.wait(1)
			giveTool(player)
		end)

		giveTool(player)
	end
end)

MarketplaceService.PromptGamePassPurchaseFinished:Connect(function(player, passId, purchased)
	if passId == GAMEPASS_ID and purchased then
		giveTool(player)
	end
end)
