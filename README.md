# spsc-ringbuffer-testbench-hs
testbench for lock-free haskell spsc-ringbuffer libraries.

the repo contains the following test profiles, each setup so as to ensure that the ring buffer itself never fills up:

1. _**Debug**_\
   runs the bench with logging for debugging. 
2. _**Control**_
   runs the bench without calling the push/pop methods. for use in determining language-specific overhead.
4. _**Raw**_\
   runs the only the workload of the benchmark. no timing. intended for use with perf.
5. _**Timed**_\
   runs a timed workload. t0 is taken at the instant before the producer (and therefore strictly before the consumer) starts. t1 is taken at the instant after the consumer (and therefore strictly after the producer) finishes. the result is time taken to complete some given number of operations (write + corresponding read). intended to determine throughput.
6. _**Sampled**_\
   the features of timed + samples per-operation latencies. the intention behind timing this test itself is for comparison against a pure timed test to determine the magnitude of the observer effect (how measurements are affected from sampling per-op latencies).





the library must define the module `RingBuffer.SPSC` with the following export list:

1. SPSCRingBuffer\
   A type to refer to the ring buffer.

3. initRb :: Word -> IO (SPSCRingBuffer a)\
   A method to initialize the ring buffer, that takes an ring buffer size input of type `Word`. The type stored in the ring buffer itself, `a`, is inferred from the caller.

4. pushRb :: SPSCRingBuffer a -> a -> IO ()\
   A method to write items to the ring buffer.

5. popRb :: SPSCRingBuffer a -> IO a\
  A method to read items from the ring buffer.

6. destroyRb :: SPSCRingBuffer a -> IO ()\
  A method to free manually-allocated resources related to the ring buffer. If the implementation relies only on managed memory, make this do nothing.

