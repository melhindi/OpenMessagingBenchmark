# Questions
- Does Pulsar publish async (ie. 50k msg/sec publish rate async)?
- Partitions vs Topics

# Measurements
- 1) 0 consumer, 1 producer, 1 topic, 1 partition vs vary msg size (100byte, 500byte, 1KB, 2KB)
- 2) IO measurments (iostat -s SamplingRate -x DevicePath -c )

- 3)  1 topic -> increase producer - is there a bottleneck
=> increase partitions -> can we scale further

- 4) Preeictable latency: What happens with append latency if load is increased -> up to 70% IO utiliziation predictable latency, but high latency of 2.2 msec
- 5) How well does Bookkeeper utilize IOs (do we need smaller slices to utilize IO)
   - Vary Journal batch size and study IO utilization
   - Start with rate and batch size at which IO utilization is high around 70%
- 6) How well load balancing supported (if at all), e.g., can we use ensemble changes to implement load balancing?

- 7) Workload switch Write->read heavy, Expactation: Bookkeeper Threadpools are hard coded, no workload switch possible



# Bookkeeper Tuning
- journalBufferedWritesThreshold=524288
- journalMaxGroupWaitMSec=0
- numJournalCallbackThreads=8
- DirectIO

# TODOs
- Do not co-locate Pulsar and Bookkeeper

# Fault injection Lab group

0) Read Protocol aware recovery paper
1) Where are checksums used
2) What happens if an invalid checksum is detected
3) What happens during recovery?
4) What failures can happen without being checked by the checksums


