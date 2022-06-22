# docs-conversel-apis
Documentation of the Official Conversel API and how to use them.

# API List
## Authorization
- `/login` Returns whether the login was authorized and the token for the account.
- `/create` Creates a new account and returns whether the login was authorized and the token for the account.
- `/verify` Verifys the verification code and returns if it has been verified.
- `/is-authorized` *DEPRECATED* Returns true if the token is authorized.

## Application
- `/app/get-joined-servers` Returns all of the joined servers in the users account.
- `/app/get-friendslist` Returns all of the friends in the users account.
- `/app/add-friend` Sends a friend request to the requested user.
- `/app/remove-friend` Removes a friend from the users account.
- `/app/accept-friend-request` Accepts the received friend request.
- `/app/open-direct-message` Returns the direct message data from a direct message chat.
- `/app/open-server-text-channel` Returns the server text channel data from a server.
- `/app/get-server-data` Returns all of the server data from the database.

# Examples - Typescript
## Authorization
#### `/login`
```typescript
await Fetch("login", {
  email: emailValue,
  assword: passwordValue,
});
```
#### `/create`
```typescript
await Fetch("create", {
  username: usernameValue,
  email: emailValue,
  password: passwordValue,
  dateOfBirth: dateOfBirthValue,
});
```
#### `/verify`
```typescript
await Fetch("verify", {
  verifyCode: verifyCode,
});
```
#### `/is-authorized`
```typescript
await Fetch("is-authorized", {
  token: token,
});
```
#### `/app/get-joined-servers`
```typescript
await Fetch("/app/get-joined-servers", {
  token: token,
});
```
#### `/app/get-friendslist`
```typescript
await Fetch("app/get-friendslist", {
  token: token,
});
```
#### `/app/add-friend`
```typescript
await Fetch("app/add-friend", {
  token: token,
  username: username
});
```
#### `/app/remove-friend`
```typescript
await Fetch("app/remove-friend", {
  token: token,
  friendId: friendId
});
```
#### `/app/accept-friend-request`
```typescript
await Fetch("app/accept-friend-request", {
  token: token,
  requestId: requestId
});
```
#### `/app/open-direct-message`
```typescript
await Fetch("app/open-direct-message", {
  token: token,
  friendId: friendId
});
```
#### `/app/open-server-text-channel`
```typescript
await Fetch("app/open-server-text-channel", {
  token: token,
  channelId: channelId,
  serverId: serverId
});
```
#### `/app/get-server-data`
```typescript
await Fetch("app/get-server-data", {
  token: token,
  serverId: serverId
});
```

### Function being used
```typescript
async function Fetch<T = any>(
    api: string,
    data: any,
    customUrl?: string
): Promise<T> {
    const environment = window.Main.getEnv();
    let respFormatted;
    await fetch(
        environment !== "production"
            ? "http://localhost:3000/" + api
            : "https://conversel.com/" + api || customUrl,
        {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(data),
        }
    ).then((res) => {
        respFormatted = res.json();
    });
    return respFormatted;
}
```
