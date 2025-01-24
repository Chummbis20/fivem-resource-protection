# FiveM Resource Protection Guide
A comprehensive guide on protecting FiveM resources from unauthorized access, including anti-dump measures.

## Basic Resource Protection

### Using Wildcards in Manifest
```lua
client_scripts {
   "client/*.lua"  -- Loads all .lua files in client folder
}

-- OR for nested folders:
client_scripts {
   "client/**/*.lua"  -- Loads from all subfolders
}
```

## Anti-Dump Implementation
### Required Files:
1. public.lua:

```lua
local WaitUntilLoaded = true

RegisterNetEvent('QBCore:Client:OnPlayerLoaded', function()
    CreateThread(function()
        while WaitUntilLoaded do Wait(0) end
        TriggerEvent('YourTriggerNameInsideClient.lua')
    end)
end)

AddEventHandler('onResourceStart', function(resource)
    if resource == GetCurrentResourceName() then
        Wait(100)
        CreateThread(function()
            while WaitUntilLoaded do Wait(0) end
            TriggerEvent('YourTriggerNameInsideClient.lua')
        end)
    end
end)

function LoadSuccess()
    WaitUntilLoaded = false
end

exports('LoadSuccess', LoadSuccess)
```

2. Add to end of client.lua:

```lua
CreateThread(function() 
    exports['your-resource-name']:LoadSuccess() 
end)
```

## Important Notes:
- Don't use same event names across resources
- Recommended format: resource-name:client:OnPlayerLoaded
- Consider network changes that may trigger script reloads
- Use queue system for timeout issues
- Keep resources separate in anti-dump configs

## Standard Protection Methods
### Load Order Control

```lua
client_scripts {
    "client/main.lua",      -- Loads first
    "client/secondary.lua"   -- Loads second
}

-- With partial hiding:
client_scripts {
    "client/main.l*a",      
    "client/secondary.l*a"   
}
```

### Protected Folder Structure

```lua
ResourceName/
├── fxmanifest.lua
├── j8k2m/          
│   ├── x7d9f.lua   
│   └── y8h3k.lua   
└── p4n5r/          
    └── q2w3e.lua
```

### Best Practices
1. Move sensitive logic server-side
2. Use randomized folder/file names
3. Break code into multiple files
4. Avoid common names
5. Use nested structures
6. Implement authentication
7. Use NUI blocker
8. Implement proper loading checks

### Additional Security
- Use HTTPS/TLS
- Implement rate limiting
- Server-side validation
- Auth/authorization
- Code obfuscation
- Queue systems for timeouts
- Network change handling

Remember: Combine these methods with anti-dump protection for maximum security.
