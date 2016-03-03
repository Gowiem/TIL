# Append items to a List bin type

This was surprisingly hard to find in the Aerospike Docs, but is relatively simple.

```java
public void appendToListBin(pKey, binKey, newBinValue) {
    Operation op = ListOperation.append(binKey, Value.get(newBinValue));

    WritePolicy wPolicy = new WritePolicy();
    wPolicy.recordExistsAction = RecordExistsAction.UPDATE;

    try {
        aerospikeClient.operate(wPolicy, pKey, op);
    } catch (AerospikeException e) {
        e.printStackTrace();
    }
}
```