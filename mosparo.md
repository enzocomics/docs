# Integrating Mosparo with Next.js
What I've done & learned so far:
- I installed the [JS API client](https://github.com/mosparo/js-api-client)
- I had to create my own type definitions by referencing the source files
- The frontend Mosparo script had to be placed in the onReady prop of a Next.js `Script` component:
```Typescript
<Script
  src={mosparoURL + "/build/mosparo-frontend.js}
  onReady={() => {
    var m = new mosparo()
  }}
>
```
- The submit verification HAS to be inside the server action that submits the form. Attempting to do so from a client component will throw a CORS error
- Importing instead of requiring the script should work as long as all the types are correctly defined (well, duh. But it still was a whole process)
- The server action form looks like:
```Typescript
import mosparoClient from "@mosparo/api-client"

export async function formSubmit(comment: CommentDataType): Promise<JSON> {
  const client = new mosparoClient.Client(mosparoURL, mosparoPublicKey, mosparoPrivateKey, {})

  return client.verifySubmission(
    comment,
    comment.mosparoSubmitToken,
    comment.mosparoValidationToken
).then(
  (VerificationResult: any) => { // I don't know how to type the VerificationResult
    if (VerificationResult.isSubmittable()) {
      // Success
    } else {
      // Failure
    }
  }
})
```
