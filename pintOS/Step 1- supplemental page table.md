1. create supplemental page table

````C


## Why separate them?

| Function | Called by | Purpose |
|----------|-----------|---------|
| `vm_claim_page(va)` | Page fault handler | "I just need this VA to work" |
| `vm_do_claim_page(page)` | Internal / direct page setup | "I already have the page struct" |
| `vm_get_frame()` | `vm_do_claim_page` | "I need raw physical memory" |



## Lazy loading example
```
1. Process loads executable
   → vm_alloc_page() for each segment
   → Pages in SPT, but NO physical memory yet

2. Process runs, accesses code at 0x400000
   → CPU: "No mapping!" → PAGE FAULT

3. Page fault handler:
   → vm_claim_page(0x400000)
   → Finds page in SPT
   → vm_do_claim_page(page)
   → vm_get_frame() — get physical frame
   → pml4_set_page() — create mapping
   → swap_in() — load code from executable file

4. Return from fault, retry instruction
   → Now 0x400000 works!
```

````

![[Pasted image 20251201140137.png]]
````C
Why UNINIT exists
┌─────────────────────────────────────────────────────────────┐
│                    BEFORE PAGE FAULT                         │
│                                                              │
│   Page is UNINIT:                                           │
│   - No physical frame yet                                    │
│   - No data loaded                                          │
│   - Just stores "what to do when claimed"                   │
│     (initializer function, aux data, etc.)                  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
                           │
                           │ Page fault occurs
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    AFTER PAGE FAULT                          │
│                                                              │
│   swap_in() is called                                        │
│       ↓                                                      │
│   uninit_initialize() runs                                   │
│       ↓                                                      │
│   Calls stored initializer (anon_initializer or             │
│                             file_backed_initializer)        │
│       ↓                                                      │
│   Page becomes ANON or FILE                                 │
│                                                              │
└─────────────────────────────────────────────────────────────┘

````