# Users

User information such as friends and profile data are made available to both the server and client. You can access the User API using `Platform.server.user` and `Platform.client.user`.

## Common Patterns

```typescript
// Get a users friends
const response = await Platform.client.user.GetFriends();
if (!response.success) return;

// List of objects containing user data such as username and status text.
const friends = response.data;
```
