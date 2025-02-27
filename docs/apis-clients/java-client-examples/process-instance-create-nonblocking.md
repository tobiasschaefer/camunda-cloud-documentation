---
id: process-instance-create-nonblocking
title: "Create non-blocking process instances"
description: "Let's analyze the prerequisites and code to create non-blocking process instances with Java."
---

## Prerequisites

1. Run the Zeebe broker with endpoint `localhost:26500` (default).
2. Run the [deploy a process example](process-deploy.md).

## NonBlockingProcessInstanceCreator.java

[Source on GitHub](https://github.com/camunda-cloud/zeebe/blob/develop/samples/src/main/java/io/camunda/zeebe/example/process/NonBlockingProcessInstanceCreator.java)

```java
long instancesCreating = 0;

while (instancesCreating < numberOfInstances) {
    // this is non-blocking/async => returns a future
    final ZeebeFuture<ProcessInstanceEvent> future =
        client.newCreateInstanceCommand().bpmnProcessId(bpmnProcessId).latestVersion().send();

    // could put the future somewhere and eventually wait for its completion

    instancesCreating++;
}
```
