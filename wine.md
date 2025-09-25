# Wine
Usually, Wine Just Works.

```sh
wine ./path/to/exe
```

## Observations
Wine creates a dummy Windows filesystem at a location called the "Wine Prefix".
This is controllable by the `WINEPREFIX` environment variable.
This defaults to `~/.wine`.

The `WINEDLLOVERRIDES` environment variable selects specific DLLs to be substituted.
I still don't know how this works, and in practice applications that need these DLLs seem to just fail
to load necessary DLLs if they're in this list.

## 32-bit wine
To run 32-bit wine, you need to set the `WINEARCH` variable to "win32" and use a different `WINEPREFIX`.
I just used `~/.wine32` for my 32-bit wine prefix.

Note that pre-release or extended versions of wine, like `wine-10.15-staging-tkg`,
don't necessarily support win32.

### Example: Warcraft 3 world editor
I just need to record my pain getting this program to work ~~to heal from the pain~~
so I can recreate it if I lose my config.

I initially got the Warcraft 3 world editor running under Lutris, sharing the same `WINEPREFIX` as
Battle.net, Starcraft 2, and Warcraft 3.
Note running Warcraft 3 (v1.30) for the first time prompted me for my CD keys, which I entered.

On trying to run WorldEdit, the program would start, and then crash after 5~10s.
Checking the log in Lutris/when running from command line showed:
```
012c:err:virtual:allocate_virtual_memory out of memory for allocation, base (nil) size 00691000
012c:err:vulkan:allocate_external_host_memory NtAllocateVirtualMemory failed
012c:err:virtual:allocate_virtual_memory out of memory for allocation, base (nil) size 00691000
012c:err:vulkan:allocate_external_host_memory NtAllocateVirtualMemory failed
012c:err:virtual:allocate_virtual_memory out of memory for allocation, base (nil) size 00691000
012c:err:vulkan:allocate_external_host_memory NtAllocateVirtualMemory failed
012c:err:virtual:allocate_virtual_memory out of memory for allocation, base (nil) size 00691000
012c:err:vulkan:allocate_external_host_memory NtAllocateVirtualMemory failed
012c:err:virtual:allocate_virtual_memory out of memory for allocation, base (nil) size 00691000
012c:err:vulkan:allocate_external_host_memory NtAllocateVirtualMemory failed
err:   DxvkMemoryAllocator: Memory allocation failed
err:     Size:      6881792
err:     Alignment: 16
err:     Mem types: 0,7,8,9,10
err:   Heap  Size (MiB)  Allocated   Used        Reserved    Budget
err:    0:     8192          30          18          18        7060      
err:    1:    24032          32           8           8       24032      
err:    2:      246           4           2           6         238      
terminate called after throwing an instance of 'dxvk::DxvkError'
Monitored process exited.
```

Investigation showed this is a long-standing issue with DXVK wherein the Vulkan calls just take more memory
than the OpenGL calls they emulate, and so some 32-bit applications would just run out of address space.
There are apparently all sorts of flags to try to get these programs to behave,
variants on `FORCE_LARGE_ADDRESS_AWARE`, and someone even posted some code for patching the flags in an .exe
to work with this. But from what I could tell, the "large address aware" flag was already set in WorldEdit.

Running with DXVK turned off resulted in the program running, but getting ~4 frames per second.
It was not particularly usable. Checking the logs again revealed this ominous message:
```
0168:fixme:opengl:wow64_map_buffer Doing a copy of a mapped buffer (expect performance issues)
```

And I was sure seeing "performance issues".

This fixme comes from the code for Wine's opengl.dll translation code.
I saw recently-merged PRs touching code in that area,
but wasn't able to figure out if there was something I could do to avoid the expensive copy.

As a second-to-last resort (last resort being to use a Windows VM),
I tried making a new win32 wineprefix and running in there.
Note I had to first run warcraft 3 in that wineprefix to enter the CD keys,
as WorldEdit does not prompt you for them and simply fails if they haven't been entered.

Sure enough, it worked! :D
