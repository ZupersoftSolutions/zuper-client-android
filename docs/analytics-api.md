## Table of contents

- [Job Stats](#job-stats-)

#### Job Stats

The following method is used to fetch Jobs from Zuper.

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

