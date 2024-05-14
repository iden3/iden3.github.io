

type: `https://didcomm.org/report-problem/2.0/problem-report`

Message to report problems between parties. This message follows the DIDComm protocol. 

```json
{
  "pthid": "<parent thread>", // The thread in which the problem occurred
  "ack": [
    "<previous report message id 1>",
    "<previous report message id 2>",
    "..."
  ],
  "body": {
    "code": "e.xfer.remote-server-down",
    "comment": "Remote server {1} is down when connecting from {2}",
    "args": [
      "https://remote-server.org",
      "https://my-server.org"
    ],
    "escalate_to": "admin@remote-server.org"
  },
  "from": "did:polygonid:polygon:mumbai:2qJG6RYgN1u6v7JAYSdfixSwktnZ7hMzd4t21SCdNu",
  "to": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp"
}
```

| Field       | Description                                                                  | Type | Required |
|-------------|------------------------------------------------------------------------------| --- | -- |
| pthid       | Parent thread                                                                | string | ✅ |
| ack         | List of IDs of previous messages that triggered this one                     | string |  ❌ |
| code        | Problem code (See Problem Codes section)                                     | string |  ✅ |
| comment     | Human-friendly text describing the problem. Can include {1} placeholders {2} | string |  ❌ |
| args        | List of arguments matching the placeholders in comment field                 | string |  ❌ |
| escalate_to | URI where more help about the problem could be received                      | string |  ❌ |


- **Example of report problem message:**
    
    ```json
    {
        "id": "6f269888-0f93-4012-9f9d-e1da9896f261",
        "typ": "application/iden3comm-plain-json",
        "type": "https://didcomm.org/report-problem/2.0/problem-report",
        "thid": "18633df6-3a6d-4a40-88bc-7fe7792f6375",
        "pthid": "5333207e-7338-4ab3-ac34-bf9a20dab6ab",
        "ack": [
            "23b610b3-aec8-4d1c-8a75-3b22e5483fb0",
            "86fe7cc6-adcd-4530-8e07-92c060b427c8"
        ],
        "body": {
            "code": "e.xfer.remote-server-down",
            "comment": "Remote server {1} is down when connecting from {2}",
            "args": [
                "https://remote-server.org",
                "https://my-server.org"
            ],
            "escalate_to": "admin@remote-server.org"
        },
        "from": "did:polygonid:polygon:mumbai:2qJG6RYgN1u6v7JAYSdfixSwktnZ7hMzd4t21SCdNu",
        "to": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp"
    }
    ```
  
  - **Problem codes:**

Problem codes are lower kebab-case. They are structured as a sequence of tokens delimited by '.' char.
Structure: 

A code is usually structured as 3 or more sections separated by '.'.

`(e|w).(p|m|state-name).descriptor1[.descriptor2[.descriptor3]...]`

The first section is called the sorted and should be 'e' for errors or 'w' for warnings.

Second section is the scope of the problem. Scope gives the sender's point of view of what context should be reverted 

Scope can be 'p' for protocol, 'm' for message, or a formal state name from the sender's state machine in the active protocol. This state machine is the scope to which the sender protocol will revert to.

This section is a collection of descriptors that give more context to the problem. Descriptors are separated by '.' char.



examples:
```
e.xfer.remote-server-down
e.trust.user-not-found
e.p.req-time.expired
```