Interactive debugging is excellent for reproducible local behavior. Production failures require evidence that survives after the request and process are gone.

That is where structured logs become essential.

A useful log entry should describe an event through stable fields rather than only through a sentence. The operation name, request identifier, user or tenant identifier where appropriate, entity identifier, status, duration, and safe error category allow logs to be searched and connected later.

```
logger.info({
  event: "invoice_generation_completed",
  requestId,
  operationId,
  invoiceId,
  organizationId,
  durationMs,
});
```

The correlation identifier is what turns separate entries into one story. A request ID can connect middleware, controller, service, and response logs. An operation ID can continue across retries, queues, and background processing even when each delivery receives a new request ID.

Without correlation, production debugging becomes a search through approximate timestamps and similar messages. A single customer action may generate hundreds of unrelated-looking lines across several processes.

Good logs also require restraint. Recording entire request bodies, authentication headers, user entities, or external responses can expose sensitive data and create so much noise that the useful evidence becomes difficult to find.

I want logs to answer what happened, which operation it belonged to, and where the operation stopped progressing. I do not want them to become an uncontrolled copy of production data.
