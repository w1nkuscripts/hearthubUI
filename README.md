# hearthubUI

Heart UI Library

GUI-библиотека для Roblox в стиле читов CS / Minecraft: тёмная тема, розовый акцент, пиксельный шрифт.

RightShift (меняется) открывает и закрывает меню
Перетаскивание за шапку, растягивание за правый нижний угол
Вкладки сверху листаются колесом мыши, плавное подчёркивание под выбранной вкладкой
Поиск функций (лупа), бинды (шестерёнка: toggle / hold / always)
Watermark и Keybind list
Подключение
lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/<ник>/<репо>/main/source.lua"))()

Полный пример: example.lua.

Window
lua
local Window = Library:New({
    Name = "heart",                        -- название в watermark
    Suffix = ".hub",                       -- розовая часть названия
    ToggleKey = Enum.KeyCode.RightShift,
    Size = Vector2.new(560, 420),
    Accent = Color3.fromRGB(255, 105, 165),
    Font = Enum.Font.Arcade,
})

Window:Destroy()
Tabs / SubTabs / Sections
lua
local Tab = Window:CreateTab("Rage")          -- алиас AddTab
local Sub = Tab:CreateSubTab("Aim")           -- алиас AddSubTab
local Sec = Sub:CreateSection("Aimbot", "Left") -- "Left" | "Right" (по умолчанию чередуются)
Elements
lua
Sec:CreateToggle(name, { Default = false, Keybind = true, Mode = "hold", Flag = "x", Callback = fn })
Sec:CreateSlider(name, { Min = 0, Max = 100, Default = 50, Suffix = "%", Rounding = 0, Flag = "x", Callback = fn })
Sec:CreateDropdown(name, { Options = {...}, Default = "A" | {"A","B"}, Multi = false, Flag = "x", Callback = fn })
Sec:CreateButton(name, fn)
Sec:CreateLabel(text)

Методы элементов: :Set(value, silent), Dropdown:Get(), Toggle:SetKey(KeyCode|nil), Toggle:SetMode("toggle"|"hold"|"always").

Flags

Если у элемента указан Flag, значение доступно из любого места:

lua
Library.Flags.silent_aim   -- true / false
Library.Flags.hitboxes     -- { "Head", "Chest" }
Library.Options.hit_chance:Set(80)
Бинды

Шестерёнка у тоггла (Keybind = true) открывает окно бинда.

toggle - клавиша переключает функцию
hold - функция включена, пока клавиша зажата
always - функция всегда включена
Esc или Backspace убирают клавишу

Включённые функции с биндом показываются в Keybind list в виде silent aim (held), (toggled) или (always).

HUD
lua
Library:SetWatermarkVisible(true)
Library:SetKeybindListVisible(true)
Library:Unload()
