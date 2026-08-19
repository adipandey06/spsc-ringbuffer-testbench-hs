# spsc-ringbuffer-testbench-hs
testbench code for haskell spsc-ringbuffer libraries.

the library must define the module `RingBuffer.SPSC` with the following export list:

1. SPSCRingBuffer\
   A type to refer to the ring buffer.\

3. initRb :: Word -> IO (SPSCRingBuffer a)\
   A method to initialize the ring buffer, that takes an ring buffer size input of type `Word`. The type stored in the ring buffer itself, `a`, is inferred from the caller.\

4. pushRb :: SPSCRingBuffer a -> a -> IO ()\
   A method to write items to the ring buffer.\

5. popRb :: SPSCRingBuffer a -> IO a\
  A method to read items from the ring buffer.\

6. destroyRb :: SPSCRingBuffer a -> IO ()\
  A method to free manually-allocated resources related to the ring buffer. If the implementation relies only on managed memory, make this do nothing.\

