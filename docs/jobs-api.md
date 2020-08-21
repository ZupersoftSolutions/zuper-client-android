## Jobs API's

- [Jobs](#jobs-)
- [Job Details](#job-details)

#### Jobs

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

#### Job Details

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

| **Parameter** | **Type** | **Description**                                          |
| ------------- | -------- | -------------------------------------------------------- |
| jobUid        | `String` | From Date should be in format yyyy-MM-dd. Ex: 2020-03-04 |

**Response Field Summary**

| **Field** | **Type** | **Description**                                              |
| --------- | -------- | ------------------------------------------------------------ |
| job       | ZuperJob | Response include job UID, work order number, job statuses, customer detail, recurring job details, assigned users, custom fields and more |