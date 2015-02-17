### Random key

If no partition key provided, the producer will use a random partition to send message, and save the partition to cache, then use that partition from cache afterwards.
[producer only sending to one partition](http://www.makingitscale.com/2013/kafka-producers-only-sending-to-one-partition.html)

```scala
if(key == null) {
  // If the key is null, we don't really need a partitioner
  // So we look up in the send partition cache for the topic to decide the target partition
  val id = sendPartitionPerTopicCache.get(topic)
  id match {
    case Some(partitionId) =>
      // directly return the partitionId without checking availability of the leader,
      // since we want to postpone the failure until the send operation anyways
      partitionId
      ...
  }
}
```