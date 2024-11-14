local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- ฟังก์ชันสำหรับโจมตีผู้เล่นด้วยการโจมตีที่กำหนด
local function attackPlayer(player)
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        local humanoid = player.Character.Humanoid

        -- ข้อกำหนดสำหรับการโจมตีแต่ละอาวุธ
        local weapons = {
            "Lightning Sword",
            "Saber",
            "Triple Katana",
            "Real Knife",
            "Dual Sword",
            "True Youru",
            "Amethyst Scythe",
            "Bisento",
            "Cursed Scythe",
            "Elucidator",
            "Youru",
            "Epic Sword"
        }

        for _, weaponName in ipairs(weapons) do
            local weapon = LocalPlayer.Character:FindFirstChild(weaponName)
            if weapon and weapon:FindFirstChild("Remote") then
                local args = {
                    [1] = "Slash",
                    [2] = { humanoid }
                }
                weapon.Remote.Weapon_Event:FireServer(unpack(args))
            end
        end

        -- การโจมตี Limitless
        if LocalPlayer.Character:FindFirstChild("Limitless") then
            local args = {
                [1] = "Attack",
                [2] = { humanoid }
            }
            LocalPlayer.Character.Limitless.Remote.Combat_Event:FireServer(unpack(args))
        end
    end
end

-- ฟังก์ชันออโต้รันสำหรับโจมตีผู้เล่นทั้งหมด
local function autoAttack()
    while true do
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then -- ข้ามตัวผู้เล่นที่กำลังใช้งาน
                attackPlayer(player) -- การโจมตีผู้เล่น
            end
        end
        wait(0.5) -- รอ 0.5 วินาทีก่อนที่จะโจมตีซ้ำ
    end
end

-- เรียกใช้งานฟังก์ชันออโต้รัน
autoAttack()
