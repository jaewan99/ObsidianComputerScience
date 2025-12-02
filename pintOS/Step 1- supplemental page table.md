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

````C
SPT table

SPT (supplemental_page_table)
 │
 └──► hash (spt_hash)
       │
       └──► buckets (array of lists)
             │
             ├──► bucket[0] ──► hash_elem ──► hash_elem ──► ...
             │                     │              │
             │                     ▼              ▼
             │                   page           page
             │
             ├──► bucket[1] ──► list_elem ──► ...
             │                     │
             │                     ▼
             │                   page
             │
             ├──► bucket[2] ──► (empty)
             │
             └──► bucket[n] ──► ...
````


````C
PHYS_BASE (0xC0000000) - USER STACK - Visual (stack grows downward)
    ↓
+------------------+ 
| "/bin/ls\0"      |  ← argument strings
| "foo\0"          |
| "bar\0"          |
+------------------+
| (padding)        |  ← word align
+------------------+
| NULL             |  ← argv[3]
| ptr to "bar"     |  ← argv[2]
| ptr to "foo"     |  ← argv[1]
| ptr to "/bin/ls" |  ← argv[0]
+------------------+
| argv (ptr)       |  ← points to argv[0]
+------------------+
| argc = 3         |
+------------------+
| return addr = 0  |
+------------------+  ← esp starts here

this chunk is created per page - 4kb
````