FiveM Resource Protection Guide
This guide explains methods to protect your FiveM resources from unauthorized access and copying.
Basic Resource Protection
Using Wildcards in Manifest
The manifest file (fxmanifest.lua) can use wildcards to avoid listing exact filenames:
luaCopyclient_scripts {
    "client/*.lua"  -- Loads all .lua files in client folder
}

-- OR for nested folders:
client_scripts {
    "client/**/*.lua"  -- Loads from all subfolders
}
Load Order Control
When scripts depend on each other, maintain load order while using protection:
luaCopy-- Standard loading:
client_scripts {
    "client/main.lua",      -- Loads first
    "client/secondary.lua"   -- Loads second
}

-- With partial name hiding:
client_scripts {
    "client/main.l*a",      -- Still loads first
    "client/secondary.l*a"   -- Still loads second
}
Folder Structure Protection
Example of protected folder structure:
CopyResourceName/
├── fxmanifest.lua
├── j8k2m/           -- Client folder (instead of "client")
│   ├── x7d9f.lua   -- Main file
│   └── y8h3k.lua   -- Secondary file
└── p4n5r/          -- Server folder (instead of "server")
    └── q2w3e.lua
Best Practices

Move sensitive logic to server-side
Use randomized folder and file names
Break code into multiple files
Avoid common names like "main" or "utils"
Use nested folder structures
Implement proper authentication for server-client communication

Implementation Tips
Basic Folder Protection
luaCopy-- In fxmanifest.lua
client_scripts {
    "ElkQlJ9REJ/*.lua"  -- Random folder name
}

server_scripts {
    "cJbaXhuIp1/*.lua"  -- Random folder name
}
Nested Structure
luaCopyclient_scripts {
    "client/*/*.lua"     -- Matches files in subfolders
    "client/**/*.lua"    -- Matches files in all nested folders
}
Additional Security Measures

Use HTTPS/TLS for network communications
Implement rate limiting
Validate all input server-side
Use proper authentication and authorization
Consider code obfuscation for critical client-side scripts

Remember: The best protection is keeping sensitive logic server-side where it cannot be accessed by clients.
