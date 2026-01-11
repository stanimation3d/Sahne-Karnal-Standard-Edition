Karnal64 API User Manual (Standard Edition)
Karnal64 is a high-performance kernel interface providing low-level hardware interaction, kernel memory management, and multi-language support (C, C++, Rust, D). This manual is based on the source code analysis of the Sahne-Karnal-Standard-Edition project.

1. Architectural Overview
The Karnal64 architecture is built upon three primary pillars:
* Hardware Abstraction (Hardware Specific): Definitions specific to CPU and system architecture.
* Memory Management (Kernel Memory): Kernel-level addressing and memory block management.
* Multi-Language Support: Ability to perform system calls from different languages via FFI (Foreign Function Interface).

2. Core Components
A. Hardware Specifications (hardware_specific.h)
This file defines the physical limits and architectural parameters of the system.
* Address Width: 64-bit addressing standards.
* Register Definitions: Macros for hardware-level register access.

B. Kernel Memory Management (kernel_memory.h)
Determines the system's memory map and allocation strategies.
* "kmemory_init()": Initializes the kernel memory pool.
* "kmemory_alloc(size)": Allocates a secure memory block of the specified size.
* "kmemory_map(phys, virt)": Maps a physical address to a virtual address.

3. Language-Specific Usage Examples
Karnal64 features a "Polyglot" structure. Here are basic initialization examples across different languages:
C and C++ Usage (main.c / main.cpp)
In C-based languages, you can access the kernel loop by including the header files.
```
#include "karnal.h"
#include "hardware_specific.h"

int main() {
    // 1. Initialize the system
    karnal_init();
    
    // 2. Hardware Compatibility Check
    if (check_hardware_compatibility()) {
        karnal_start_loop();
    }
    
    return 0;
}
```

Rust Usage (karnal64.rs)
The Rust side wraps system calls safely, typically within unsafe blocks for FFI.
```
// Access via karnal64.rs
use karnal64_sys::*;

fn main() {
    unsafe {
        karnal64::initialize();
        karnal64::memory_map_setup();
    }
}
```

D Language Usage (main.d)
The D language performs direct function calls thanks to C ABI compatibility.
```
import karnal.api;

void main() {
    initKarnal();
    scope(exit) cleanupKarnal();
    
    runSystemTasks();
}
```

4. API Function Reference
| Function | Description | Source File |
| karnal_init() | Initializes all kernel subsystems | karnal.h |
| get_hw_info() | Returns current hardware information (CPU, RAM) | hardware_specific.h |
| kmem_reserve() | Reserves a specific memory region | kernel_memory.h |
| karnal_shutdown() | Safely shuts down the system | karnal.h |

5. Compilation and Integration
To include Karnal64 in your project, add the relevant source files to your build chain.

Compiling with GCC/Clang:
"gcc main.c -I./src/karnal64 -o karnal_test"


Rust Integration:
Include it as a module by specifying the local path in your Cargo.toml.

6. Important Notes and Warnings
* Memory Safety: Manual cleanup (free) is required for allocations made via kernel_memory.h (except for the Rust layer abstraction).
* Hardware Dependency: Definitions in hardware_specific.h must be adjusted according to the target platform (x86_64, ARM, etc.).
* Synchronization: In multi-core systems, use the locking mechanisms provided in karnal.h.
