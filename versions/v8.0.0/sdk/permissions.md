---
title: Permissions
old_permalink: /versions/v8.0.0/sdk/permissions.html
previous___FILE: ./location.md
---

When it comes to adding functionality that can access potentially sensitive information on a user's device, such as their location, or possibly send them possibly unwanted push notifications, you will need to ask the user for their permission first. Unless you've already asked their permission, then no need. And so we have the `Permissions` module.

### `Exponent.Permissions.getAsync(type)`

Determines whether your app has already been granted access to the provided permission type.

#### Arguments

-   **type (_string_)** -- The name of the permission.

#### Returns

Returns a `Promise` that is resolved with the information about the permission, including status, expiration and scope (if it applies to the permission type).

#### Example

```javascript
async function alertIfRemoteNotificationsDisabledAsync() {
  const { Permissions } = Exponent;
  const { status } = await Permissions.getAsync(Permissions.REMOTE_NOTIFICATIONS);
  if (status !== 'granted') {
    alert('Hey! You might want to enable notifications for my app, they are good.');
  }
}
```

### `Exponent.Permissions.askAsync(type)`

Prompt the user for a permission. If they have already granted access, response will be success.

#### Arguments

-   **type (_string_)** -- The name of the permission.

#### Returns

Returns a `Promise` that is resolved with the information about the permission, including status, expiration and scope (if it applies to the permission type).

#### Example

```javascript
async function getLocationAsync() {
  const { Location, Permissions } = Exponent;
  const { status } = await Permissions.askAsync(Permissions.LOCATION);
  if (status === 'granted') {
    return Location.getCurrentPositionAsync({enableHighAccuracy: true});
  } else {
    throw new Error('Location permission not granted');
  }
}
```

### `Exponent.Permissions.REMOTE_NOTIFICATIONS`

The permission type for push notifications.

### `Exponent.Permissions.LOCATION`

The permission type for location access.
