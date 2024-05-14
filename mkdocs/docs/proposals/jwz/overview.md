# JSON Web Zero-knowledge


# Summary

JSON Web Zero-knowledge (JWZ) is an open standard for representing messages proven by zero-knowledge technology.

This specification of the JSON Web Zero-knowledge standard that relay on a draft of the JWM standard and JWT (RFC7519) standards.

While having a lot in common, JWZ  has different intents from JWT and JWM. A JWM is about a sender creating a message composed of attributes, where the message is destined for a recipient or recipients. Whereas a JWT is about an issuer expressing claims about a subject to an audience. See the section in Section 2.1 of [[JWM](https://tools.ietf.org/id/draft-looker-jwm-01.html#attributes-thread-id)]. JWZ is about proving the message that can be represented as JWT claims and JWM attributes set.

While a JWM leverages JSON Web Signature (JWS) and or JSON Web Encryption (JWE) to achieve digital signing, integrity protection, and confidentiality JWZ utilizes zero-knowledge technologies.

Its main goal is to provide a new way of interaction between users by providing data integrity of the message, anonymity of sender public keys, and providing helpful metadata among the message.

# Definition

JWZ consists of three parts separated by dots (.), which are:

- Header
- Payload message
- Zero-knowledge proof

- Example of compacted jwz token:

    ```jsx
    eyJhbGciOiJncm90aDE2IiwiY2lyY3VpdElkIjoiYXV0aFYyIiwiY3JpdCI6WyJjaXJjdWl0SWQiXSwidHlwIjoiYXBwbGljYXRpb24vaWRlbjMtemtwLWpzb24ifQ.eyJpZCI6ImM3NTUzZWFhLWFlY2QtNGRjNi1iMDU3LWExY2IyOWNhZGJmYiIsInR5cCI6ImFwcGxpY2F0aW9uL2lkZW4zLXprcC1qc29uIiwidHlwZSI6Imh0dHBzOi8vaWRlbjMtY29tbXVuaWNhdGlvbi5pby9hdXRob3JpemF0aW9uLzEuMC9yZXNwb25zZSIsInRoaWQiOiI0MGNjMDllYS04NWRhLTQ4Y2UtOTE4OC1jNDQwZDM1MWVlNTMiLCJib2R5Ijp7ImRpZF9kb2MiOnsiY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvbnMvZGlkL3YxIl0sImlkIjoiZGlkOnBvbHlnb25pZDpwb2x5Z29uOmFtb3k6MnFhUG9kMVF4bzlVS1R6UjdLM1lvNjNnTlJGSEJtOThiaDFrMVNFWTZ4Iiwic2VydmljZSI6W3siaWQiOiJkaWQ6cG9seWdvbmlkOnBvbHlnb246YW1veToycWFQb2QxUXhvOVVLVHpSN0szWW82M2dOUkZIQm05OGJoMWsxU0VZNngjcHVzaCIsInR5cGUiOiJwdXNoLW5vdGlmaWNhdGlvbiIsInNlcnZpY2VFbmRwb2ludCI6Imh0dHBzOi8vcHVzaC1zdGFnaW5nLnBvbHlnb25pZC5jb20vYXBpL3YxIiwibWV0YWRhdGEiOnsiZGV2aWNlcyI6W3siY2lwaGVydGV4dCI6InZWTGpGWFRGVldEbE5DUStFV0dhNlRiRFNEUWx5UDVrSXpwSWFNc0d3UlRWRy93YmExN2ExZnNNWFRtQjhFbnZpWThKUmZWQjF6MDN2dyszVzhicFJnWEdNeXJONXpOekdOSVh0WjNTUVdmb3VUVkZhV2NFWTVSWW1PV05JcW5SeDdTU0lDQUsxZTlSbzdEVTNOdHJJUldJWkFqWVBmaG5zOVNiU2pGYnpmWmhvckJuSHFzK3dlRWxSRUQrZUc4alpOc0NIYWRzY3Ewcm4zSGFIZkJrTi9NYnc3allSaW9vY2xmREorSDIwaUZKODVWWVRJSTdhb3RaMWxkS3hTbDhvb2NwTXJVeTJRaktENVRXVTliZ0tZOE15YWhpQjJUN0p5Qk1zWDgxQzlZbW1sbTJFTHl2aWh0cmMwTDhKQlJFOUhMdERLWnpwK2pwbDdMK205WE1ka3AxejVMKzVYNG9lTmdHOXBCODFzTVJhTzROM1RTVU1XY0dmejhQdDRHZktDUFdFaThmUWdmeGU1UUFoQUcra3ZVSzRDbVBsdk9hUExURTVJM3JpWnRZcklJdDh0eDVLNnkrUmJyaThXV1h0M2h3dU10MjVuZk9qdnpNcjVxSE5TRTZSc2xPczdpNGNpMHhlLy9mbEdSck1qZEJ0bEhEZExwT3ptdTZlSlA5WHJtVzcwL2haVFBveXhRc1BFTUFrNVl0L1hMSm9VYmJQcXVtYmZ3MURhbFRHaFdla3A3Ri9mUDZ6Kzd1Tyt2b2piUzZnemVDUEhyUHkrTkJydHJsSmRnQi8zVEEyclJ1KytlaFpWMDh0WndWK01qNGRkVjZmcnd3UnVKQTNXWm83RWhRV2ppNEJYeTNudzE0bVNZTEVwb01qWTdwZnJSNHMrTW9qakoxRE9vPSIsImFsZyI6IlJTQS1PQUVQLTUxMiJ9XX19XX0sIm1lc3NhZ2UiOm51bGwsInNjb3BlIjpbeyJwcm9vZiI6eyJwaV9hIjpbIjE1MzYwNzE5OTc0MzY0NzMzNzIzNTMyMjI2NTM1MTAyNjY1NzQ1NjEyMDY4Nzg4NzczMjk2MzYxMDc0NjM1MzA2NTc1NDUyMTM3ODA1IiwiMTU2Mzg5MzI4MDc2Nzc5NjA5NzAzMTgzNDI0NTE0NTkwNDcxMzI4ODI0NjgyNTQ4NTU2MTU0NzUwNDcwNjg2MjQxMzY3ODU2ODUyODQiLCIxIl0sInBpX2IiOltbIjEyMjQzODg4NjM2MTY1MzQzMDA0NjM1NjE3ODA0MDY5NTk1ODI1MjExMDUyMTgwOTY3MDcwNDc1MDY3NzE4OTc3MjUyMzE5NTEwNDE2IiwiNDU0OTU0MDc2OTQ3NzExMDA2MzY0MDk1OTIyNTExMTQ0MjQ5NDg3MTQ5OTE2Njc3NDE5Mzg0NzkxNjg4MjAxNzUwMDI1ODg4NTIxOSJdLFsiMjIwMDQ0ODAxNTAwOTcwNzg0NjM0NTMxODI5NzUzODE3ODkyMTY3ODEzODUzNzI2MjA0MjY0MjIzNjY0NjEzNzQ5ODQ3MjQyMjEyMCIsIjcyNTg5ODk5MTUwMzg2MzE3Mzk1NzIwNjkyMzU0Mjg2ODcyMjQwNzkwODMwMzk5NTQzMTgxNzk0NzkyNzc3MDYzNDg4MjAzMTI3NTYiXSxbIjEiLCIwIl1dLCJwaV9jIjpbIjQ5NTU3NTc3MDEzNjI3MzMyMDgzNjY1MDQ2NTU5NDI2NzI5NDc5NDI4NjYxNjEyNTQ5NzgwMjE5OTA5NjM5Nzc4MzQ4MDU0MDU5NzEiLCIxOTQ3OTA5MzE1MzYxNTIxNDI5MTAyMjM4NTk2Mjg0MjQ3NDcwOTEzNTg5NDcxMDU3NjA1NDE1MjI0MTUzMzU4NzQyNDEwNDYwOTkzMiIsIjEiXSwicHJvdG9jb2wiOiJncm90aDE2IiwiY3VydmUiOiJibjEyOCJ9LCJwdWJfc2lnbmFscyI6WyIxIiwiMjQyNDI2NDIxMjgzNjA2MTMyNTQ4NDQwMDM1NTk3Nzg0NDAwNzU5NDEyMjU0MTY4ODUxMDMwMzYwMDAxNTExNDQ0MTk2OTMzMTQiLCIxNzAxNjE3MjUyODk5MDc2MzkzNzE0MjQyODE5MjU0MzY4Mzg0NTYzNzYzNjY4NTE5OTA0ODIyOTY4MTc2MDI5MjYxMTYwMTA2MDQ0OSIsIjAiLCIwIiwiMCIsIjEiLCIxIiwiMjU4MjczNDkwNzI2MDkzMTY5NDczOTY5Nzk4Mjg1MTg3ODk3MDA5MTIzNTE2MjM1MDYwODA0ODkzODk4OTQwNzUyNjg2NjYxMTQiLCIxIiwiMTA4NTM1NzM1ODU2MDA2NjcwODQ0ODQ2MjQ2NTkwNjg5MzQ3Mzg0ODAwOTkxMjgyNzIwMjg2MjA0MjI3NjQzODg1OTU1MTgzNzA3MzAiLCIxNzEyMzI3NTM1IiwiMTA2MjI4MTM4NTc4MTc3MzcxNTU2NDEyNzM0NzQwMjU5NDA1MDczIiwiODI2MjE1ODQ1MTY0NTQ2NjExNjgyNTYwMTg4OTUwMzAxMTkwODYwMTE1NTE3NTI3Mzk2ODY4NjkwMDk2MjI1MTk0MzQ5NjIyNzAzOSIsIjAiLCIxIiwiMSIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjEiLCIyNTgyNzM0OTA3MjYwOTMxNjk0NzM5Njk3OTgyODUxODc4OTcwMDkxMjM1MTYyMzUwNjA4MDQ4OTM4OTg5NDA3NTI2ODY2NjExNCIsIjAiXSwiaWQiOjEsImNpcmN1aXRJZCI6ImNyZWRlbnRpYWxBdG9taWNRdWVyeVYzLWJldGEuMSJ9XX0sImZyb20iOiJkaWQ6cG9seWdvbmlkOnBvbHlnb246YW1veToycWFQb2QxUXhvOVVLVHpSN0szWW82M2dOUkZIQm05OGJoMWsxU0VZNngiLCJ0byI6ImRpZDpwb2x5Z29uaWQ6cG9seWdvbjphbW95OjJxVjlRWGRoWFhtTjVzS2pOMVl1ZU1qeGdSYm5KY0VHSzJrR3B2azNjcSJ9.eyJwcm9vZiI6eyJwaV9hIjpbIjE1MjgzNTY1OTE3NzI5NTE2ODAwMjY5ODM5ODQ3NTk0MDUyOTY5NjIzMDM0NjU2NzM3MzExNjQxNTM2NzM0NzQzOTE4ODYxNTI2MjM4IiwiMTU3OTcyNDMzMzkyNTY3NjUyOTMyNjg2NjE1MDg1Mjg0NTA4MjY4MzIyOTQ2NzUwNDU1ODkzNjcxNjcwMDg1NjU4ODU5MjIyMzc4MCIsIjEiXSwicGlfYiI6W1siMTg3ODU4NjY0MDQ3MjU5MTA3NDc1NTI0MjgyMzU5ODIyNzAzNTQzODgxMjIyODMwNjI4ODg0MDg2ODQ2NTYxMDY1MzYyMTUyODkzOCIsIjMyMTQ0MTcxNTEwMzcxNzg3ODAzMTc1MDQ2NjMwNDI0NjM2MjI3NzczODYzODA0MjY1NjQyMjkxMTkxNjg0MzE2MzkwNzUyNDYwMTciXSxbIjEwNTQ2NDI4NTI2OTQyNTI1NTI2ODA2ODkyMDkyMDcxMTI2MDc5MjY0MjA4MDkyMzQ3NTE3MDQwNDY2MDU5NTczMjc0MTMzMzI1MCIsIjIwNDE1NjQ0MTMxMzczNDE3ODYwOTQ5MTU0NzcxNTAwMzMwMjc0ODYzMTQzMDIzNzI2MzgwNjgyNTQ5MTM4ODY4MjgwNzEyOTc3MzM2Il0sWyIxIiwiMCJdXSwicGlfYyI6WyI2ODUwNjU2MzQ1MzI0NDA5NTAxODE3NzM1NDgzNzcwMTcxMzg5MjAxNzgwODEzNjM1ODQ5MzYzOTk0NjE0MzE3NTQ5OTU2Mzc4MDc5IiwiNDIwNDc3Njc4MzQyNzQxODEzMDg0MjYxOTk1Nzk5NTg5Njk5MTY5NTE5MzkwNDkxNzY0NjU2NzE3NjU4Njk2NDkzMjU0OTkwOTAxMSIsIjEiXSwicHJvdG9jb2wiOiJncm90aDE2IiwiY3VydmUiOiJibjEyOCJ9LCJwdWJfc2lnbmFscyI6WyIyNDI0MjY0MjEyODM2MDYxMzI1NDg0NDAwMzU1OTc3ODQ0MDA3NTk0MTIyNTQxNjg4NTEwMzAzNjAwMDE1MTE0NDQxOTY5MzMxNCIsIjExMjA4NDE2ODYzNjgwNTgxMTk5MDg0ODg4MzI0MzExNTI5MzkwNTg4NDc1MjE3MDQyMjY3OTI3NzkxMjI5MTU1NDQ2MTU1MjMxMTA4IiwiMTc4NDk5ODE3MjA2MzQyMTI4MDI2NjQxODk5Mjk2NzExNDA3NjI1NTc0ODMyMzY3MDgwOTc3MjM4ODQxNzI2NDExMjQ2OTEyMjIyOTgiXX0
    ```
    Link to  [web parser](eyJhbGciOiJncm90aDE2IiwiY2lyY3VpdElkIjoiYXV0aFYyIiwiY3JpdCI6WyJjaXJjdWl0SWQiXSwidHlwIjoiYXBwbGljYXRpb24vaWRlbjMtemtwLWpzb24ifQ).

**The first part** - headers:

- base 64 encoded headers

  `eyJhbGciOiJncm90aDE2IiwiY2lyY3VpdElkIjoiYXV0aFYyIiwiY3JpdCI6WyJjaXJjdWl0SWQiXSwidHlwIjoiYXBwbGljYXRpb24vaWRlbjMtemtwLWpzb24ifQ`


```json
{
    "alg": "groth16",
    "circuitId": "authV2",
    "crit": [
        "circuitId"
    ],
    "typ": "application/iden3-zkp-json"
}
```

**alg** - is a zero-knowledge algorithm that is used for proof generation.

**circuitId** - is a circuit that is used for proof generation. For authentication - auth circuit must be used.

**crit -** describes the list of header keys that the verifier must support.

**typ -** is the media type of the message. In our case, it’s the protocol type of packed message *application/iden3-zkp-json*

**The second part** - message:

```jsx
eyJpZCI6ImM3NTUzZWFhLWFlY2QtNGRjNi1iMDU3LWExY2IyOWNhZGJmYiIsInR5cCI6ImFwcGxpY2F0aW9uL2lkZW4zLXprcC1qc29uIiwidHlwZSI6Imh0dHBzOi8vaWRlbjMtY29tbXVuaWNhdGlvbi5pby9hdXRob3JpemF0aW9uLzEuMC9yZXNwb25zZSIsInRoaWQiOiI0MGNjMDllYS04NWRhLTQ4Y2UtOTE4OC1jNDQwZDM1MWVlNTMiLCJib2R5Ijp7ImRpZF9kb2MiOnsiY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvbnMvZGlkL3YxIl0sImlkIjoiZGlkOnBvbHlnb25pZDpwb2x5Z29uOmFtb3k6MnFhUG9kMVF4bzlVS1R6UjdLM1lvNjNnTlJGSEJtOThiaDFrMVNFWTZ4Iiwic2VydmljZSI6W3siaWQiOiJkaWQ6cG9seWdvbmlkOnBvbHlnb246YW1veToycWFQb2QxUXhvOVVLVHpSN0szWW82M2dOUkZIQm05OGJoMWsxU0VZNngjcHVzaCIsInR5cGUiOiJwdXNoLW5vdGlmaWNhdGlvbiIsInNlcnZpY2VFbmRwb2ludCI6Imh0dHBzOi8vcHVzaC1zdGFnaW5nLnBvbHlnb25pZC5jb20vYXBpL3YxIiwibWV0YWRhdGEiOnsiZGV2aWNlcyI6W3siY2lwaGVydGV4dCI6InZWTGpGWFRGVldEbE5DUStFV0dhNlRiRFNEUWx5UDVrSXpwSWFNc0d3UlRWRy93YmExN2ExZnNNWFRtQjhFbnZpWThKUmZWQjF6MDN2dyszVzhicFJnWEdNeXJONXpOekdOSVh0WjNTUVdmb3VUVkZhV2NFWTVSWW1PV05JcW5SeDdTU0lDQUsxZTlSbzdEVTNOdHJJUldJWkFqWVBmaG5zOVNiU2pGYnpmWmhvckJuSHFzK3dlRWxSRUQrZUc4alpOc0NIYWRzY3Ewcm4zSGFIZkJrTi9NYnc3allSaW9vY2xmREorSDIwaUZKODVWWVRJSTdhb3RaMWxkS3hTbDhvb2NwTXJVeTJRaktENVRXVTliZ0tZOE15YWhpQjJUN0p5Qk1zWDgxQzlZbW1sbTJFTHl2aWh0cmMwTDhKQlJFOUhMdERLWnpwK2pwbDdMK205WE1ka3AxejVMKzVYNG9lTmdHOXBCODFzTVJhTzROM1RTVU1XY0dmejhQdDRHZktDUFdFaThmUWdmeGU1UUFoQUcra3ZVSzRDbVBsdk9hUExURTVJM3JpWnRZcklJdDh0eDVLNnkrUmJyaThXV1h0M2h3dU10MjVuZk9qdnpNcjVxSE5TRTZSc2xPczdpNGNpMHhlLy9mbEdSck1qZEJ0bEhEZExwT3ptdTZlSlA5WHJtVzcwL2haVFBveXhRc1BFTUFrNVl0L1hMSm9VYmJQcXVtYmZ3MURhbFRHaFdla3A3Ri9mUDZ6Kzd1Tyt2b2piUzZnemVDUEhyUHkrTkJydHJsSmRnQi8zVEEyclJ1KytlaFpWMDh0WndWK01qNGRkVjZmcnd3UnVKQTNXWm83RWhRV2ppNEJYeTNudzE0bVNZTEVwb01qWTdwZnJSNHMrTW9qakoxRE9vPSIsImFsZyI6IlJTQS1PQUVQLTUxMiJ9XX19XX0sIm1lc3NhZ2UiOm51bGwsInNjb3BlIjpbeyJwcm9vZiI6eyJwaV9hIjpbIjE1MzYwNzE5OTc0MzY0NzMzNzIzNTMyMjI2NTM1MTAyNjY1NzQ1NjEyMDY4Nzg4NzczMjk2MzYxMDc0NjM1MzA2NTc1NDUyMTM3ODA1IiwiMTU2Mzg5MzI4MDc2Nzc5NjA5NzAzMTgzNDI0NTE0NTkwNDcxMzI4ODI0NjgyNTQ4NTU2MTU0NzUwNDcwNjg2MjQxMzY3ODU2ODUyODQiLCIxIl0sInBpX2IiOltbIjEyMjQzODg4NjM2MTY1MzQzMDA0NjM1NjE3ODA0MDY5NTk1ODI1MjExMDUyMTgwOTY3MDcwNDc1MDY3NzE4OTc3MjUyMzE5NTEwNDE2IiwiNDU0OTU0MDc2OTQ3NzExMDA2MzY0MDk1OTIyNTExMTQ0MjQ5NDg3MTQ5OTE2Njc3NDE5Mzg0NzkxNjg4MjAxNzUwMDI1ODg4NTIxOSJdLFsiMjIwMDQ0ODAxNTAwOTcwNzg0NjM0NTMxODI5NzUzODE3ODkyMTY3ODEzODUzNzI2MjA0MjY0MjIzNjY0NjEzNzQ5ODQ3MjQyMjEyMCIsIjcyNTg5ODk5MTUwMzg2MzE3Mzk1NzIwNjkyMzU0Mjg2ODcyMjQwNzkwODMwMzk5NTQzMTgxNzk0NzkyNzc3MDYzNDg4MjAzMTI3NTYiXSxbIjEiLCIwIl1dLCJwaV9jIjpbIjQ5NTU3NTc3MDEzNjI3MzMyMDgzNjY1MDQ2NTU5NDI2NzI5NDc5NDI4NjYxNjEyNTQ5NzgwMjE5OTA5NjM5Nzc4MzQ4MDU0MDU5NzEiLCIxOTQ3OTA5MzE1MzYxNTIxNDI5MTAyMjM4NTk2Mjg0MjQ3NDcwOTEzNTg5NDcxMDU3NjA1NDE1MjI0MTUzMzU4NzQyNDEwNDYwOTkzMiIsIjEiXSwicHJvdG9jb2wiOiJncm90aDE2IiwiY3VydmUiOiJibjEyOCJ9LCJwdWJfc2lnbmFscyI6WyIxIiwiMjQyNDI2NDIxMjgzNjA2MTMyNTQ4NDQwMDM1NTk3Nzg0NDAwNzU5NDEyMjU0MTY4ODUxMDMwMzYwMDAxNTExNDQ0MTk2OTMzMTQiLCIxNzAxNjE3MjUyODk5MDc2MzkzNzE0MjQyODE5MjU0MzY4Mzg0NTYzNzYzNjY4NTE5OTA0ODIyOTY4MTc2MDI5MjYxMTYwMTA2MDQ0OSIsIjAiLCIwIiwiMCIsIjEiLCIxIiwiMjU4MjczNDkwNzI2MDkzMTY5NDczOTY5Nzk4Mjg1MTg3ODk3MDA5MTIzNTE2MjM1MDYwODA0ODkzODk4OTQwNzUyNjg2NjYxMTQiLCIxIiwiMTA4NTM1NzM1ODU2MDA2NjcwODQ0ODQ2MjQ2NTkwNjg5MzQ3Mzg0ODAwOTkxMjgyNzIwMjg2MjA0MjI3NjQzODg1OTU1MTgzNzA3MzAiLCIxNzEyMzI3NTM1IiwiMTA2MjI4MTM4NTc4MTc3MzcxNTU2NDEyNzM0NzQwMjU5NDA1MDczIiwiODI2MjE1ODQ1MTY0NTQ2NjExNjgyNTYwMTg4OTUwMzAxMTkwODYwMTE1NTE3NTI3Mzk2ODY4NjkwMDk2MjI1MTk0MzQ5NjIyNzAzOSIsIjAiLCIxIiwiMSIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjAiLCIwIiwiMCIsIjEiLCIyNTgyNzM0OTA3MjYwOTMxNjk0NzM5Njk3OTgyODUxODc4OTcwMDkxMjM1MTYyMzUwNjA4MDQ4OTM4OTg5NDA3NTI2ODY2NjExNCIsIjAiXSwiaWQiOjEsImNpcmN1aXRJZCI6ImNyZWRlbnRpYWxBdG9taWNRdWVyeVYzLWJldGEuMSJ9XX0sImZyb20iOiJkaWQ6cG9seWdvbmlkOnBvbHlnb246YW1veToycWFQb2QxUXhvOVVLVHpSN0szWW82M2dOUkZIQm05OGJoMWsxU0VZNngiLCJ0byI6ImRpZDpwb2x5Z29uaWQ6cG9seWdvbjphbW95OjJxVjlRWGRoWFhtTjVzS2pOMVl1ZU1qeGdSYm5KY0VHSzJrR3B2azNjcSJ9
```

- In current example is an [authorization response iden3comm message](https://iden3-communication.io/authorization/1.0/response/)

    ```json
    {
      "id": "c7553eaa-aecd-4dc6-b057-a1cb29cadbfb",
      "typ": "application/iden3-zkp-json",
      "type": "https://iden3-communication.io/authorization/1.0/response",
      "thid": "40cc09ea-85da-48ce-9188-c440d351ee53",
      "body": {
        "did_doc": {
          "context": [
            "https://www.w3.org/ns/did/v1"
          ],
          "id": "did:polygonid:polygon:amoy:2qaPod1Qxo9UKTzR7K3Yo63gNRFHBm98bh1k1SEY6x",
          "service": [
            {
              "id": "did:polygonid:polygon:amoy:2qaPod1Qxo9UKTzR7K3Yo63gNRFHBm98bh1k1SEY6x#push",
              "type": "push-notification",
              "serviceEndpoint": "https://push-staging.polygonid.com/api/v1",
              "metadata": {
                "devices": [
                  {
                    "ciphertext": "vVLjFXTFVWDlNCQ+EWGa6TbDSDQlyP5kIzpIaMsGwRTVG/wba17a1fsMXTmB8EnviY8JRfVB1z03vw+3W8bpRgXGMyrN5zNzGNIXtZ3SQWfouTVFaWcEY5RYmOWNIqnRx7SSICAK1e9Ro7DU3NtrIRWIZAjYPfhns9SbSjFbzfZhorBnHqs+weElRED+eG8jZNsCHadscq0rn3HaHfBkN/Mbw7jYRiooclfDJ+H20iFJ85VYTII7aotZ1ldKxSl8oocpMrUy2QjKD5TWU9bgKY8MyahiB2T7JyBMsX81C9Ymmlm2ELyvihtrc0L8JBRE9HLtDKZzp+jpl7L+m9XMdkp1z5L+5X4oeNgG9pB81sMRaO4N3TSUMWcGfz8Pt4GfKCPWEi8fQgfxe5QAhAG+kvUK4CmPlvOaPLTE5I3riZtYrIIt8tx5K6y+Rbri8WWXt3hwuMt25nfOjvzMr5qHNSE6RslOs7i4ci0xe//flGRrMjdBtlHDdLpOzmu6eJP9XrmW70/hZTPoyxQsPEMAk5Yt/XLJoUbbPqumbfw1DalTGhWekp7F/fP6z+7uO+vojbS6gzeCPHrPy+NBrtrlJdgB/3TA2rRu++ehZV08tZwV+Mj4ddV6frwwRuJA3WZo7EhQWji4BXy3nw14mSYLEpoMjY7pfrR4s+MojjJ1DOo=",
                    "alg": "RSA-OAEP-512"
                  }
                ]
              }
            }
          ]
        },
        "message": null,
        "scope": [
          {
            "proof": {
              "pi_a": [
                "15360719974364733723532226535102665745612068788773296361074635306575452137805",
                "15638932807677960970318342451459047132882468254855615475047068624136785685284",
                "1"
              ],
              "pi_b": [
                [
                  "12243888636165343004635617804069595825211052180967070475067718977252319510416",
                  "4549540769477110063640959225111442494871499166774193847916882017500258885219"
                ],
                [
                  "2200448015009707846345318297538178921678138537262042642236646137498472422120",
                  "7258989915038631739572069235428687224079083039954318179479277706348820312756"
                ],
                [
                  "1",
                  "0"
                ]
              ],
              "pi_c": [
                "4955757701362733208366504655942672947942866161254978021990963977834805405971",
                "19479093153615214291022385962842474709135894710576054152241533587424104609932",
                "1"
              ],
              "protocol": "groth16",
              "curve": "bn128"
            },
            "pub_signals": [
              "1",
              "24242642128360613254844003559778440075941225416885103036000151144419693314",
              "17016172528990763937142428192543683845637636685199048229681760292611601060449",
              "0",
              "0",
              "0",
              "1",
              "1",
              "25827349072609316947396979828518789700912351623506080489389894075268666114",
              "1",
              "10853573585600667084484624659068934738480099128272028620422764388595518370730",
              "1712327535",
              "106228138578177371556412734740259405073",
              "8262158451645466116825601889503011908601155175273968686900962251943496227039",
              "0",
              "1",
              "1",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "1",
              "25827349072609316947396979828518789700912351623506080489389894075268666114",
              "0"
            ],
            "id": 1,
            "circuitId": "credentialAtomicQueryV3-beta.1"
          }
        ]
      },
      "from": "did:polygonid:polygon:amoy:2qaPod1Qxo9UKTzR7K3Yo63gNRFHBm98bh1k1SEY6x",
      "to": "did:polygonid:polygon:amoy:2qV9QXdhXXmN5sKjN1YueMjxgRbnJcEGK2kGpvk3cq"
    }
    ```

  **from**  -  sender identity. To is a verifier identityifer.

  **id** - unique message id

  **thid -** id of message thread (must be the same as in the request)

  **message -** signed message

  **scope -** array of generated claim proofs


**The third part** - proof:

```jsx
eyJwcm9vZiI6eyJwaV9hIjpbIjE1MjgzNTY1OTE3NzI5NTE2ODAwMjY5ODM5ODQ3NTk0MDUyOTY5NjIzMDM0NjU2NzM3MzExNjQxNTM2NzM0NzQzOTE4ODYxNTI2MjM4IiwiMTU3OTcyNDMzMzkyNTY3NjUyOTMyNjg2NjE1MDg1Mjg0NTA4MjY4MzIyOTQ2NzUwNDU1ODkzNjcxNjcwMDg1NjU4ODU5MjIyMzc4MCIsIjEiXSwicGlfYiI6W1siMTg3ODU4NjY0MDQ3MjU5MTA3NDc1NTI0MjgyMzU5ODIyNzAzNTQzODgxMjIyODMwNjI4ODg0MDg2ODQ2NTYxMDY1MzYyMTUyODkzOCIsIjMyMTQ0MTcxNTEwMzcxNzg3ODAzMTc1MDQ2NjMwNDI0NjM2MjI3NzczODYzODA0MjY1NjQyMjkxMTkxNjg0MzE2MzkwNzUyNDYwMTciXSxbIjEwNTQ2NDI4NTI2OTQyNTI1NTI2ODA2ODkyMDkyMDcxMTI2MDc5MjY0MjA4MDkyMzQ3NTE3MDQwNDY2MDU5NTczMjc0MTMzMzI1MCIsIjIwNDE1NjQ0MTMxMzczNDE3ODYwOTQ5MTU0NzcxNTAwMzMwMjc0ODYzMTQzMDIzNzI2MzgwNjgyNTQ5MTM4ODY4MjgwNzEyOTc3MzM2Il0sWyIxIiwiMCJdXSwicGlfYyI6WyI2ODUwNjU2MzQ1MzI0NDA5NTAxODE3NzM1NDgzNzcwMTcxMzg5MjAxNzgwODEzNjM1ODQ5MzYzOTk0NjE0MzE3NTQ5OTU2Mzc4MDc5IiwiNDIwNDc3Njc4MzQyNzQxODEzMDg0MjYxOTk1Nzk5NTg5Njk5MTY5NTE5MzkwNDkxNzY0NjU2NzE3NjU4Njk2NDkzMjU0OTkwOTAxMSIsIjEiXSwicHJvdG9jb2wiOiJncm90aDE2IiwiY3VydmUiOiJibjEyOCJ9LCJwdWJfc2lnbmFscyI6WyIyNDI0MjY0MjEyODM2MDYxMzI1NDg0NDAwMzU1OTc3ODQ0MDA3NTk0MTIyNTQxNjg4NTEwMzAzNjAwMDE1MTE0NDQxOTY5MzMxNCIsIjExMjA4NDE2ODYzNjgwNTgxMTk5MDg0ODg4MzI0MzExNTI5MzkwNTg4NDc1MjE3MDQyMjY3OTI3NzkxMjI5MTU1NDQ2MTU1MjMxMTA4IiwiMTc4NDk5ODE3MjA2MzQyMTI4MDI2NjQxODk5Mjk2NzExNDA3NjI1NTc0ODMyMzY3MDgwOTc3MjM4ODQxNzI2NDExMjQ2OTEyMjIyOTgiXX0
```

- In the current example, it’s a proof of authV2  circuit

    ```json
    {
      "proof": {
        "pi_a": [
          "15283565917729516800269839847594052969623034656737311641536734743918861526238",
          "1579724333925676529326866150852845082683229467504558936716700856588592223780",
          "1"
        ],
        "pi_b": [
          [
            "1878586640472591074755242823598227035438812228306288840868465610653621528938",
            "3214417151037178780317504663042463622777386380426564229119168431639075246017"
          ],
          [
            "105464285269425255268068920920711260792642080923475170404660595732741333250",
            "20415644131373417860949154771500330274863143023726380682549138868280712977336"
          ],
          [
            "1",
            "0"
          ]
        ],
        "pi_c": [
          "6850656345324409501817735483770171389201780813635849363994614317549956378079",
          "4204776783427418130842619957995896991695193904917646567176586964932549909011",
          "1"
        ],
        "protocol": "groth16",
        "curve": "bn128"
      },
      "pub_signals": [
        "24242642128360613254844003559778440075941225416885103036000151144419693314",
        "11208416863680581199084888324311529390588475217042267927791229155446155231108",
        "17849981720634212802664189929671140762557483236708097723884172641124691222298"
      ]
    }
    ```

  **pub_signals**  - UserID (profile or genesis)  Challenge ( payload hash ),  GistRoot


We create a zero-knowledge proof by proving the specific message using the auth v2 circuit and its inputs.

To prepare auth circuit inputs user need to prove that BJJ key is not revoked and included in the latest user state, also user needs to sign a challenge with corresponding private key.

```go
type AuthInputs struct {

	GenesisID    *core.ID `json:"genesisID"`
	ProfileNonce *big.Int `json:"profileNonce"`

	AuthClaim *core.Claim `json:"authClaim"`

	AuthClaimIncMtp    *merkletree.Proof `json:"authClaimIncMtp"`
	AuthClaimNonRevMtp *merkletree.Proof `json:"authClaimNonRevMtp"`
	TreeState          TreeState         `json:"treeState"`

	GISTProof GISTProof `json:"gistProof"`

	Signature *babyjub.Signature `json:"signature"`
	Challenge *big.Int           `json:"challenge"`
}
```

- as a Challenge field, we use the message hash,
- Gist Proof represents inclusion of the user non-genesis state to the global identity state or non-inclusion of genesis user state.

More about how GIST is [here](https://docs.iden3.io/protocol/spec/#gist-new).

reference implementations:
go:  [https://github.com/iden3/go-jwz/blob/main/jwz.go](https://github.com/iden3/go-jwz/blob/main/jwz.go)

js-jwz :[https://github.com/iden3/js-jwz](https://github.com/iden3/js-jwz)

```go
// Token represents a JWZ Token.
type Token struct {
	ZkProof *types.ZKProof // The third segment of the token.  Populated when you Parse a token

	Alg       string // fields that are part of headers
	CircuitID string // id of a circuit that will be used for proving

	Method ProvingMethod // proving method to create a zkp

	raw rawJSONWebZeroknowledge // The raw token.  Populated when you Parse a token

	inputsPreparer ProofInputsPreparerHandlerFunc
}
```

**ZKProof** - object that contains proof and pub signals

**Alg** / **CircuitId** - zkp alg and circuit that is used for proof generation.

**Method**  - Proving method to create a proven token.

**raw** - rawJSONWebZeroknowledge raw representation of the token

**inputsPreparer** - handler that accepts message hash and circuit id and can generate valid circuit inputs

```go
// rawJSONWebZeroknowledge is a JSON web token with a signature presented by zero-knowledge proof
type rawJSONWebZeroknowledge struct {
	Payload   []byte                    `json:"payload,omitempty"`
	Protected []byte                    `json:"protected,omitempty"`
	Header    map[HeaderKey]interface{} `json:"header,omitempty"`
	ZKP       []byte                    `json:"zkp,omitempty"`
}
```

**Payload** - payload raw bytes (marshaled protocol message or just string)

**Header** - mapping of Header keys and their values

**ZKP**  - raw proof data

**Protected** - protected claims that were included in proof message hash. (in our case - all headers)

Methods to implement:

```go
func NewWithPayload(prover ProvingMethod, payload []byte, inputsPreparer ProofInputsPreparerHandlerFunc) (*Token, error) 
```

Creates new token, but without proof section.

```go
func (token *Token) Prove(provingKey, wasm []byte) (string, error) 
```

Prove function - accepts proving key and circuit wasm file for proof generation. Serializes headers, computes a message hash and calls **inputsPreparer** to prepare inputs. Then it calls the defined proving method and returns a compacted token with zkp.

### Algorithm for message hash generation:

Message hash is a big integer that represents Poseidon Hash. This Poseidon Hash is created using the following algorithm:

1. Prepare hash to sign: it’s *`is ASCII(BASE64URL(UTF8(JWZ Protected Header)) || '.' || BASE64URL(JWZ Payload)).`*
2. Get serialized representation of Prepared message.
3. Get the sha256 hash of the message, swap endianness, and create a big Integer.
4. If the resulting hash is not a Q field, defined by the go-iden-crypto library, then divide resulted in a big integer from this hash by Q.
5. Make Poseidon hash of resulting big Integer.

```go
func (token *Token) Verify(verificationKey []byte) (bool, error) 
```

Verify accepts verification key as a parameter,  computes message hash, and calls defined proving method for proof verification.

```go
func (token *Token) FullSerialize() (string, error)
```

Returns serialization of rawJSONWebZeroknowledge as JSON string

```go
func (token *Token) CompactSerialize() (string, error)
```

Returns compacted form (three base64 encoded parts)

```go
func Parse(token string) (*Token, error) 
```

Parses token string (compacted or full serialized ) to Token struct.

The last crucial part to implement is ProvingMethod:

it’s a zero-knowledge protocol-specific algorithm and circuit-specific method for a proof generation:



```go
// ProvingMethod can be used to add new methods for proving or verifying tokens.
type ProvingMethod interface {
	Verify(messageHash []byte, proof *types.ZKProof, verificationKey []byte) error // Returns nil if proof is valid
	Prove(inputs []byte, provingKey []byte, wasm []byte) (*types.ZKProof, error)   // Returns proof or error
	Alg() string                                                                   // Returns the alg identifier for this method (example: 'AUTH-GROTH-16')
	CircuitID() string
}
```

in go-jwz lib, `ProvingMethodGroth16AuthV2` is defined. It uses “*groth16*” alg and “*authV2*” circuit

Prove method calculates witness and generates proof.

Verify method verifies zero-knowledge proof and checks that provided messageHash has been included in Auth Circuit public signlas.

```go
// AuthPubSignals auth.circom public signals
type AuthV2PubSignals struct {
	UserID    *core.ID         `json:"userID"`
	Challenge *big.Int         `json:"challenge"`
	GISTRoot  *merkletree.Hash `json:"GISTRoot"`
}
```
Auth Libraries to fully validate JWZ:
[https://github.com/iden3/go-iden3-auth](https://github.com/iden3/go-iden3-auth)

[https://github.com/iden3/js-iden3-auth](https://github.com/iden3/js-iden3-auth)

Circuit:
[https://docs.iden3.io/protocol/main-circuits/#authv2](https://docs.iden3.io/protocol/main-circuits/#authv2)

