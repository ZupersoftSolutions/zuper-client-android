## Jobs API's

- [Jobs](#jobs-)
- [Job Details](#job-details)
- [Job Statuses](#job-statuses)
- [Job Notes](#job-notes)
- [Job Activities](#job-activities)
- [Update Status](#update-status)
- [Reschedule Job](#reschedule-job)

### Jobs

Get jobs API provides you all the jobs with sort, filter and pagination support

```kotlin
zuperClient.getJobs(page, count, sort, jobFilter)
```

**Sample**

```kotlin
zuperClient.getJobs(page, count, sort, jobFilter).enqueue(object : ApiCallback<List<ZuperJob>>() {
    override fun onSuccess(data: List<ZuperJob>) {
        if (data.isNotEmpty()) {
            val title = data.first().jobTitle
            val workOrderNumber = data.first().workOrderNumber
            val currentStatus = data.first().currentJobStatus?.statusName
        }
    }

    override fun onError(error: Throwable) {
        // Show error message
    }
})
```

**Request Parameters**

| **Parameter** | **Type**    | **Description**                                              |
| ------------- | ----------- | ------------------------------------------------------------ |
| page          | `Int`       | Page No to fetch                                             |
| count         | `Int`       | Total records to fetch                                       |
| sort          | `JobSort`   | Jobs can be sort in Ascending/Descending and sort by Work Order Number, Priority or Scheduled start time |
| filter        | `JobFilter` | Jobs can be filtered by multiple parameters such as Job status type, Job Category, Job status, Priority and more |

**Response Field Summary**

| **Field** | **Type**   | **Description**                                              |
| --------- | ---------- | ------------------------------------------------------------ |
| job       | `ZuperJob` | Response include job UID, work order number, job statuses, customer detail |

### Job Details

Job Details API provides you all the details for the provided Job UID

```kotlin
zuperClient.getJobDetails(jobUid)
```

**Sample**

```kotlin
zuperClient.getJobDetails("12345-1234-11a1-11a1-12123132123").enqueue(object : ApiCallback<ZuperJob>() {
    override fun onSuccess(data: ZuperJob) {
    	// Show job details
        val title = data.first().jobTitle
    }

    override fun onError(error: Throwable) {
        // Show error message
    }
})
```

**Request Parameters**

| **Parameter** | **Type** | **Description**                        |
| ------------- | -------- | -------------------------------------- |
| jobUid        | `String` | Job UID for which to fetch the details |

**Response Field Summary**

| **Field** | **Type**   | **Description**                                              |
| --------- | ---------- | ------------------------------------------------------------ |
| job       | `ZuperJob` | Response include job UID, work order number, job statuses, customer detail, recurring job details, assigned users, custom fields and more |

### Job Statuses

You can fetch all the Job Statuses created under a Job Category using this API

```kotlin
zuperClient.getJobStatus(categoryUid)
```

**Sample**

```kotlin
zuperClient.getJobStatus("12345-1234-11a1-11a1-12123132123").enqueue(object : ApiCallback<JobStatusByCategory>() {
    override fun onSuccess(statuses: JobStatusByCategory) {
    	// Show statuses in dropdown
    }

    override fun onError(error: Throwable) {
        // Show error message
    }
})
```

**Request Parameters**

| **Parameter** | **Type** | **Description**                                  |
| ------------- | -------- | ------------------------------------------------ |
| categoryUid   | `String` | Job Category UID for which to fetch the statuses |

**Response Field Summary**

| **Field** | **Type**              | **Description**                                              |
| --------- | --------------------- | ------------------------------------------------------------ |
| statuses  | `JobStatusByCategory` | Response includes the list of `JobStatus` which contains status UID, name, type, remarks and other permissions such as enabled for Field Executive |

### Job Notes

This API provides you all the the notes created for a Job

```kotlin
zuperClient.getJobNotes(jobUid)
```

**Sample**

```kotlin
zuperClient.getJobNotes("12345-1234-11a1-11a1-12123132123").enqueue(object :ApiCallback<List<Note>>() {
    override fun onSuccess(data: List<Note>) {
    	// Show notes
    }

    override fun onError(error: Throwable) {
        // Show error message
    }
})
```

**Request Parameters**

| **Parameter** | **Type** | **Description**                        |
| ------------- | -------- | -------------------------------------- |
| jobUid        | `String` | Job UID for which to fetch the details |

**Response Field Summary**

| **Field** | **Type**     | **Description**                                              |
| --------- | ------------ | ------------------------------------------------------------ |
| data      | `List<Note>` | Response includes the list of `Note` which contains `note` content, note type, attachment and created by user |

### Job Activities

This API provides you all the the activities performed in a Job

```kotlin
zuperClient.getJobActivities(page, count, jobUid)
```

**Sample**

```kotlin
zuperClient.getJobActivities(1, 100, "12345-1234-11a1-11a1-12123132123")
	.enqueue(object : ApiCallback<List<JobActivity>>() {
        override fun onSuccess(data: List<JobActivity>) {
            Timber.d("test getJobActivities success")
        }

        override fun onError(error: Throwable) {
            // Show error message
        }
})
```

**Request Parameters**

| **Parameter** | **Type** | **Description**                          |
| ------------- | -------- | ---------------------------------------- |
| page          | `Int`    | Page No to fetch                         |
| count         | `Int`    | Total records to fetch                   |
| jobUid        | `String` | Job UID for which to fetch the activites |

**Response Field Summary**

| **Field** | **Type**            | **Description**                                              |
| --------- | ------------------- | ------------------------------------------------------------ |
| data      | `List<JobActivity>` | Response includes the list of `JobActivity` which contains activity type, message and created by user |

### Update Status

This API provides you all the the activities performed in a Job

```kotlin
zuperClient.updateJobStatus(params)
```

**Sample**

```kotlin
val params = JobStatusUpdateParams(
    jobUid = "80580370-a217-11e9-9dc6-696ee2a43a57",
    statusUid = "840762e0-8ad0-42d4-b61c-a5a6ebd5f092",
    remarks = "Remarks",
    freeTextRemarks = "Free text remarks",
    geoCoordinates = listOf(latitude, longitude)
)
zuperClient.updateJobStatus(params).enqueue(object : ApiCallback<Void>() {
    override fun onSuccess(data: Void?) {
        // Show success message
    }

    override fun onError(error: Throwable) {
        // Handle Error
    }
})
```

**Request Parameters**

| **Parameter** | **Type**                | **Description**                                              |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| params        | `JobStatusUpdateParams` | Job UID and status UID are mandatory. `remarks` is the remark chosen from the dropdown and `freeTextRemarks` is the user provided remarks such as from `EditText` |

**Response Field Summary**

| **Field** | **Type** | **Description**                       |
| --------- | -------- | ------------------------------------- |
| data      | `Void`   | You can simply show a success message |

### Reschedule Job

Using this API, you can update the Job Start and End Time

```kotlin
zuperClient.rescheduleJob(params)
```

**Sample**

```kotlin
val params = JobRescheduleRequest(
    jobUid = "e1f813f0-aa09-11e9-a33d-833701541d17",
    newStartDate = ZuperDateTimeUtils.formatLocalDateToUtc(Calendar.getInstance().time),
    newEndDate = ZuperDateTimeUtils.formatLocalDateToUtc(Calendar.getInstance().time),
    reason = "The customer is not available"
)
zuperClient.rescheduleJob(params).enqueue(object : ApiCallback<Void>() {
    override fun onSuccess(data: Void) {
        // Show success message
    }

    override fun onError(error: Throwable) {
        // Handle failure
    }
})
```

**Request Parameters**

| **Parameter** | **Type**               | **Description**                                              |
| ------------- | ---------------------- | ------------------------------------------------------------ |
| params        | `JobRescheduleRequest` | Provide the Job UID, start and end date in UTC Timezone formatted in ISO pattern. You can use `ZuperDateTimeUtils` for such timezone conversion and date formatting. You can also provide a `reason` for which the job is being rescheduled |

**Response Field Summary**

| **Field** | **Type** | **Description**                       |
| --------- | -------- | ------------------------------------- |
| data      | `Void`   | You can simply show a success message |

