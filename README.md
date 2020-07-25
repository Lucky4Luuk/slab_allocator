# slab_allocator

[![Build Status](https://travis-ci.org/weclaw1/slab_allocator.svg?branch=master)](https://travis-ci.org/weclaw1/slab_allocator)

[Documentation](https://docs.rs/crate/slab_allocator)

## Patches
I patched this crate to work with some of the changes made over the past 2 years to the `linked_list_allocator` crate, and certain changes made to the `alloc` crate.
There are a few comments scattered around the code to signify my small changes. Quick note: I have not properly retested everything, but these changes should be minor enough not to make a difference.

## Usage

Create a static allocator in your root module:

```rust
use slab_allocator::LockedHeap;

#[global_allocator]
static ALLOCATOR: LockedHeap = LockedHeap::empty();
```

Before using this allocator, you need to init it:

```rust
pub fn init_heap() {
    let heap_start = …;
    let heap_end = …;
    let heap_size = heap_end - heap_start;
    unsafe {
        ALLOCATOR.init(heap_start, heap_size);
    }
}
```

## License
This crate is licensed under MIT. See LICENSE for details.
