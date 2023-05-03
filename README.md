**THIS WAS COMPILED WITH HELP FROM CHATGPT**

# <h1>FreeNOS Memory Management System</h1>

## <h2>1. Identify the specific memory management system used in FreeNOS.</h2>
The specific memory management system used in FreeNOS is a type of segmentation memory management system, called split allocator memory management system. The split allocator is the **SplitAllocator.cpp** which uses four other allocators depending on the situation, which are **Allocator.cpp**, **BitAllocator.cpp**, **BubbleAllocator.cpp**, and **PoolAllocator.cpp**.
#### *- SplitAllocator.cpp*
This allocator is used to allocate both physical and virtual memory, and is the primary allocator used in FreeNOS. It uses a split allocation scheme where physical memory is allocated separately from virtual memory. This allows for efficient use of physical memory by only mapping necessary parts of virtual memory to physical memory.
#### *- Allocator.cpp*
This is the base allocator class that provides a generic interface for allocating and freeing memory. It is used as a base class for other allocators.
#### *- BitAllocator.cpp*
This allocator is used to allocate small fixed-size blocks of memory. It maintains a bitmap of the allocated and free blocks and uses bit manipulation operations to efficiently allocate and free blocks.
#### *- BubbleAllocator.cpp*
This allocator is used to allocate variable-sized blocks of memory. It uses a buddy system algorithm to manage the memory space, where memory is divided into blocks of sizes that are powers of 2. The allocator maintains a binary tree structure to track free and allocated blocks.
#### *- PoolAllocator.cpp*
This allocator is used to allocate small fixed-size blocks of memory from a pre-allocated memory pool. It is designed to be fast and efficient for allocating and freeing blocks of the same size, and can be used in situations where there are frequent allocations and deallocations of small objects.
## <h2>2. Describe its characteristics, numbers, duration, and dynamics.</h2>
#### *- Characteristics*
-   The SplitAllocator implements two separate memory ranges, one for physical memory and one for virtual memory. By using the base class Allocate.cpp and a BitAllocator.cpp object called m_alloc.
-- 
```cpp
Allocator::Result  SplitAllocator::allocate(Allocator::Range  &  phys, Allocator::Range  &  virt)`
{
	Result r =  m_alloc.allocate(phys);
	if (r == Success)
	{
		virt.address  =  toVirtual(phys.address);
		virt.size  =  phys.size;
		virt.alignment  =  phys.alignment;
		}
		return r;
}```
-   Uses a paging mechanism where memory is allocated in fixed-size pages.
-   Supports sparse allocation where the allocator can allocate memory in non-contiguous chunks.
-   Uses a callback function to report the allocated memory ranges in sparse allocation.
#### *- Duration*
#### *- Dynamics*

### 3. Provide specific code references to support your observations.
