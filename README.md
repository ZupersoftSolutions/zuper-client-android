# zuper-client-android
Zuper Client SDK lets you quickly intergrate Zuper API's in your app. 

## Table of contents
- [Prerequisites](#prerequisites-)
- [Installation](#installation-)
- [Getting started](#getting-started-)
- [API](#api-)

### Prerequisites [⤴](#table-of-contents)
* Android SDK 19 or higher
* JDK 1.8

### Installation [⤴](#table-of-contents)
Add the following dependency to your app's build.gradle file:
##### Gradle:

```gradle
implementation 'co.zuper.sdk.android:zuper-client-core:1.0.8'
```

##### or Maven:

```
<dependency>
  <groupId>co.zuper.sdk.android</groupId>
  <artifactId>zuper-client-core</artifactId>
  <version>1.0.17</version>
</dependency>
```

### Getting Started [⤴](#table-of-contents)
`ZuperClient` is the entry point to the SDK. An instance of ZuperClient can be built using `ZuperClient.Builder()` and this instance can be reused across the lifecycle of the Android App.
```kotlin
class ZuperClientSampleApp : Application() {

    lateinit var zuperClient: ZuperClient
        private set

    override fun onCreate() {
        super.onCreate()
        buildZuperClient()
    }

    private fun buildZuperClient() {
        var loggingLevel = LoggingLevel.NONE
        var environment = ZuperEnvironment.LIVE
        if (BuildConfig.DEBUG) {
            loggingLevel = LoggingLevel.BODY
            environment = ZuperEnvironment.TRAINING
        }
        zuperClient = ZuperClientBuilder()
            .context(this)
            .environment(environment)
            .loggingLevel(loggingLevel)
            .build()
    }
}
```

For more information such as session management with Zuper Client, take a look at our [Getting Started](docs/getting-started.md) guide.

### API [⤴](#table-of-contents)

* [Analytics](docs/analytics-api.md)
  * [Job Stats](docs/analytics-api.md)

* [Jobs](docs/jobs-api.md)
  * [Jobs](docs/analytics-api.md#jobs)
  * [Job Details](docs/analytics-api.md#job-details)
  * [Job Notes](docs/analytics-api.md#job-notes)
  * [Job Activities](docs/analytics-api.md#job-activities)
  * [Job Statuses](docs/analytics-api.md#job-statuses)
  * [Update Job Status](docs/analytics-api.md#update-status)
  * [Reschedule Job](docs/analytics-api.md#reschedule-job)

* [Customers](docs/customers-api.md)
  * [Customers]()
  * [Customer Details]()
  * [Customer Notes]()
* [Teams & Users](docs/teams-users-api.md)
  * [Teams]()
* [Misc](docs/misc-api.md)
  * [Add User Location]()
  * [Add Custom Activity]()