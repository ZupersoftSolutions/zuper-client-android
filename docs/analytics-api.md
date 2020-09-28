## Analytics API's

- [Job Stats](#job-stats-)

### Job Stats

Job stats API provides you the count of jobs categorised by Job Status Type, Job Status Name, Job Category, Customer Category and Customer Feedback

```kotlin
zuperClient.getJobStats(fromDate, toDate)
```

**Sample**

```kotlin
zuperClient.getJobStats("2020-01-01", "2020-03-31").enqueue(object : ApiCallback<JobAnalytics>() {
    override fun onSuccess(data: JobAnalytics) {
        val totalJobsCount = data.jobStats.totalJobs
        val inProgressCount = data.jobStats.onProgressJobs
    }

    override fun onError(error: Throwable) {
        Timber.e(error)
    }
})
```

**Request Parameters**

| **Parameter** | **Type** | **Description**                                          |
| ------------- | -------- | -------------------------------------------------------- |
| fromDate      | `String` | From Date should be in format yyyy-MM-dd. Ex: 2020-03-04 |
| toDate        | `String` | To Date should be in format yyyy-MM-dd. Ex: 2020-03-05   |

**Response Field Summary**

| **Field** | **Type**   | **Description**                              |
| --------- | ---------- | -------------------------------------------- |
| jobStats  | `JobStats` | Contains total count of jobs by status types |

