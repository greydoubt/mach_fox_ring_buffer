# mach_fox_ring_buffer
generic audio blast processing coprocessor



Mach-Ring Double Combinator Sonic-Streaming Producer-Pointer
==================================================================
Or, a simple quick and dirty circular buffer implementation for audio processing

A simple C implementation for a circular (ring) buffer. Thread-safe with a single producer and a single consumer, using OSAtomic.h primitives, and avoids any need for buffer wrapping logic by using a virtual memory map technique to place a virtual copy of the buffer straight after the end of the real buffer

Usage
-----

Initialisation and cleanup: `TPCircularBufferInit` and `TPCircularBufferCleanup` to allocate and free resources

Producing: Use `TPCircularBufferHead` to get a pointer to write to the buffer, followed by `TPCircularBufferProduce` to submit the written data.  `TPCircularBufferProduceBytes` is a convenience routine for writing data straight to the buffer

Consuming: Use `TPCircularBufferTail` to get a pointer to the next data to read, followed by `TPCircularBufferConsume` to free up the space once processed

TPCircularBuffer+AudioBufferList.(c,h) contains helper functions to queue and dequeue AudioBufferList
structures. These will automatically adjust the mData fields of each buffer to point to 16-byte aligned
regions within the circular buffer
