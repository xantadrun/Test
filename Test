local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local correctCode = "TACKLEHITBOX"
local isUnlocked = false -- ค่าเริ่มต้นยังไม่ปลดล็อก

-- สร้าง GUI หลัก
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "TackleSystem"

-- สร้าง Frame
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0.3, 0, 0.2, 0)
frame.Position = UDim2.new(0.35, 0, 0.4, 0)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

-- สร้างช่องให้ใส่รหัส
local textBox = Instance.new("TextBox", frame)
textBox.Size = UDim2.new(0.8, 0, 0.3, 0)
textBox.Position = UDim2.new(0.1, 0, 0.2, 0)
textBox.PlaceholderText = "ใส่รหัสที่นี่..."
textBox.Text = ""
textBox.TextSize = 18

-- สร้างปุ่มยืนยัน
local submitButton = Instance.new("TextButton", frame)
submitButton.Size = UDim2.new(0.8, 0, 0.3, 0)
submitButton.Position = UDim2.new(0.1, 0, 0.6, 0)
submitButton.Text = "ยืนยัน"
submitButton.TextSize = 18
submitButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)

-- สร้างปุ่มแย่งบอล (ปิดใช้งานเริ่มต้น)
local tackleButton = Instance.new("TextButton", screenGui)
tackleButton.Size = UDim2.new(0, 200, 0, 50)
tackleButton.Position = UDim2.new(0.5, -100, 0.8, 0)
tackleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
tackleButton.Text = "แย่งบอล (ล็อกอยู่)"
tackleButton.TextSize = 20
tackleButton.Font = Enum.Font.SourceSansBold
tackleButton.Visible = false

-- ฟังก์ชันตรวจสอบรหัส
submitButton.MouseButton1Click:Connect(function()
    if textBox.Text == correctCode then
        isUnlocked = true
        frame:Destroy() -- ลบหน้าต่างใส่รหัสออก
        tackleButton.Visible = true
        tackleButton.Text = "แย่งบอล"
    else
        textBox.Text = "รหัสไม่ถูกต้อง!"
    end
end)

-- ฟังก์ชันเมื่อกดปุ่มแย่งบอล
tackleButton.MouseButton1Click:Connect(function()
    if isUnlocked and character and character:FindFirstChild("TackleHitbox_RE") then
        character.TackleHitbox_RE:FireServer(workspace:WaitForChild("Ball"))
    end
end)

-- ฟังก์ชันเมื่อกดปุ่ม "E"
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.E and isUnlocked then
        local remoteEvent = character:FindFirstChild("TackleHitbox_RE")
        local ball = workspace:FindFirstChild("Ball")
        if remoteEvent and ball then
            remoteEvent:FireServer(ball)
        end
    end
end)
