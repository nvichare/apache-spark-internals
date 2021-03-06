# AccumulatorV2

`AccumulatorV2[IN, OUT]` is an [abstraction](#contract) of [accumulators](#implementations)

`AccumulatorV2` is a Java [Serializable]({{ java.api }}/java.base/java/io/Serializable.html).

## Contract

### <span id="add"> Adding Value

```scala
add(
  v: IN): Unit
```

Used when...FIXME

### <span id="copy"> Copying Accumulator

```scala
copy(): AccumulatorV2[IN, OUT]
```

Used when...FIXME

### <span id="isZero"> Is Zero Value

```scala
isZero: Boolean
```

Used when...FIXME

### <span id="merge"> Merging Updates

```scala
merge(
  other: AccumulatorV2[IN, OUT]): Unit
```

Used when...FIXME

### <span id="reset"> Resetting Accumulator

```scala
reset(): Unit
```

Used when...FIXME

### <span id="value"> Value

```scala
value: OUT
```

Used when...FIXME

## Implementations

* AggregatingAccumulator ([Spark SQL]({{ book.spark_sql }}/physical-operators/CollectMetricsExec/#accumulator))
* CollectionAccumulator
* DoubleAccumulator
* EventTimeStatsAccum ([Spark Structured Streaming]({{ book.structured_streaming }}/EventTimeStatsAccum))
* LongAccumulator
* SetAccumulator (Spark SQL)
* SQLMetric ([Spark SQL]({{ book.spark_sql }}/physical-operators/SQLMetric))

## <span id="toInfo"> toInfo

```scala
toInfo(
  update: Option[Any],
  value: Option[Any]): AccumulableInfo
```

`toInfo` determines whether the accumulator is internal based on the [name](#name) (and whether it uses the [internal.metrics](InternalAccumulator.md#METRICS_PREFIX) prefix).

`toInfo` creates an [AccumulableInfo](index.md#AccumulableInfo).

`toInfo` is used when:

* `TaskRunner` is requested to [collectAccumulatorsAndResetStatusOnFailure](../executor/TaskRunner.md#collectAccumulatorsAndResetStatusOnFailure)
* `DAGScheduler` is requested to [updateAccumulators](../scheduler/DAGScheduler.md#updateAccumulators)
* `TaskSchedulerImpl` is requested to [executorHeartbeatReceived](../scheduler/TaskSchedulerImpl.md#executorHeartbeatReceived)
* `JsonProtocol` is requested to [taskEndReasonFromJson](../history-server/JsonProtocol.md#taskEndReasonFromJson)
* `SQLAppStatusListener` ([Spark SQL]({{ book.spark_sql }}/SQLAppStatusListener/)) is requested to handle a `SparkListenerTaskEnd` event (`onTaskEnd`)

## <span id="register"> Registering Accumulator

```scala
register(
  sc: SparkContext,
  name: Option[String] = None,
  countFailedValues: Boolean = false): Unit
```

`register`...FIXME

`register` is used when:

* `SparkContext` is requested to [register an accumulator](../SparkContext.md#register)
* `TaskMetrics` is requested to [register task accumulators](../executor/TaskMetrics.md#register)
* `CollectMetricsExec` ([Spark SQL]({{ book.spark_sql }}/physical-operators/CollectMetricsExec/)) is requested for an `AggregatingAccumulator`
* `SQLMetrics` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SQLMetric)) is used to create a performance metric

## <span id="writeReplace"> writeReplace

```scala
writeReplace(): Any
```

`writeReplace`...FIXME

!!! note
    `writeReplace` is part of the [java.io.Serializable]({{ java.api }}/java.base/java/io/Serializable.html) abstraction.
    
    !!! quote
        Serializable classes that need to designate an alternative object to be used when writing an object to the stream should implement this special method with the exact signature:

        `ANY-ACCESS-MODIFIER Object writeReplace() throws ObjectStreamException;`
