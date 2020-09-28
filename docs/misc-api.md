## Other API's

- [Add Custom Activity](#add-custom-activity)
- [Add User Location](#add-user-location)

### Add Custom Activity

This API lets you add a custom activity to Zuper

```kotlin
zuperClient.addCustomActivity(module, activityType, activityAction, redirectUid, activityMessage)
```

**Sample**

```kotlin
zuperClient.addCustomActivity(
    module = ZuperModules.JOBS,
    activityType = ActivityType.CREATE,
    activityAction = ActivityAction.JOBS,
    redirectUid = "994107d0-77d7-11e8-8aa6-497f7c509174",
    activityMessage = "called the customer"
).enqueue(object : ApiCallback<Void>() {
    override fun onSuccess(data: Void) {
        // Handle Success
    }

    override fun onError(error: Throwable) {
        // Handle Error
    }
})
```

**Request Parameters**

| **Parameter**   | **Type**         | **Description**                                  |
| --------------- | ---------------- | ------------------------------------------------ |
| module          | `ZuperModules`   | Module in which the action is performed          |
| activityType    | `ActivityType`   | Type of Activity CREATE/UPDATE/DELETE            |
| activityAction  | `ActivityAction` | Redirection Action, Ex: Redirect to Jobs         |
| redirectUid     | `String`         | Redirect to UID, Ex: Job UID                     |
| activityMessage | `String`         | Custom Activity Message, Eg: Called the customer |

**Response Field Summary**

| **Field** | **Type** | **Description**                |
| --------- | -------- | ------------------------------ |
| data      | `Void`   | Simply show a success response |

### Add User Location

You can use this API to add location for tracking users

```kotlin
zuperClient.addUserLocation(params)
```

**Sample**

```kotlin
val params = AddUserLocationParams(
    trackTime = ZuperDateTimeUtils.formatLocalDateToUtc(Calendar.getInstance().time),
    latitude = 13.048871,
    longitude = 80.282442,
    signalStrength = 75, // (1 - 100)
    battery = 100, // (1 - 100)
    jobUid = "fea19530-406f-11e8-b99a-59f39b812a88", // User's current job
    remarks = "User remarks!" // Additional remarks if available
)
zuperClient.addUserLocation(params).enqueue(object : ApiCallback<Void>() {
    override fun onSuccess(data: Void) {
        // Success scenario
    }

    override fun onError(error: Throwable) {
        // Handle Error
    }
})
```

**Request Parameters**

| **Parameter** | **Type**                | **Description**                                              |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| params        | `AddUserLocationParams` | Includes latitude, longitude, signal strength in terms of percent, battery in terms of percent |

**Response Field Summary**

| **Field** | **Type** | **Description**                |
| --------- | -------- | ------------------------------ |
| data      | `Void`   | Simply show a success response |