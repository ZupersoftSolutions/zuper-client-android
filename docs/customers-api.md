## Customer API's

- [Customers](#customers)
- [Customer Detail](#customer-detail)
- [Customer Notes](#customer-notes)

### Customers

Provides the list of customers with sort, filter and pagination support

```kotlin
zuperClient.getCustomers(page, count, customerSort, customerFilter)
```

**Sample**

```kotlin
val customerSort = CustomerSort(SortType.DESC, CustomerSortOptions.CREATED_DATE)
val customerFilter = CustomerFilter(keyword = "John")
zuperClient.getCustomers(1, 10, customerSort, customerFilter)
	.enqueue(object : ApiCallback<List<Customer>>() {
        override fun onSuccess(data: List<Customer>) {
            // Show customers
        }

        override fun onError(error: Throwable) {
            // Handle failure
        }
})
```

**Request Parameters**

| **Parameter** | **Type**         | **Description**                                              |
| ------------- | ---------------- | ------------------------------------------------------------ |
| page          | `Int`            | Page No to fetch                                             |
| count         | `Int`            | Total records to fetch                                       |
| sort          | `CustomerSort`   | Customers can be sort in First Name, Last Name, No of Jobs & Created date |
| filter        | `CustomerFilter` | Jobs can be filtered by keyword, category, no of jobs and customer tags |

**Response Field Summary**

| **Field** | **Type**         | **Description**                                              |
| --------- | ---------------- | ------------------------------------------------------------ |
| data      | `List<Customer>` | Contains list of `Customer`. `Customer` model has customer name, contact details, customer category, address and tags |

### Customer Detail

This API provides you the customer details

```kotlin
zuperClient.getCustomerDetails(customerUid)
```

**Sample**

```kotlin
zuperClient.getCustomerDetails("fea19530-406f-11e8-b99a-59f39b812a88")
	.enqueue(object : ApiCallback<CustomerDetail>() {
        override fun onSuccess(data: CustomerDetail) {
            // Show customer detail
        }

        override fun onError(error: Throwable) {
            // Handle error
        }
})
```

| **Parameter** | **Type** | **Description**                             |
| ------------- | -------- | ------------------------------------------- |
| customerUid   | `String` | Customer UID for which to fetch the details |

**Response Field Summary**

| **Field** | **Type**         | **Description**                                              |
| --------- | ---------------- | ------------------------------------------------------------ |
| data      | `CustomerDetail` | Response include customer name, category, contact details, custom fields, account manager and SLA details |

### Customer Notes

This API provides you the notes added for this customer

```kotlin
zuperClient.getCustomerNotes(customerUid)
```

**Sample**

```kotlin
zuperClient.getCustomerNotes("fea19530-406f-11e8-b99a-59f39b812a88")
	.enqueue(object : ApiCallback<List<Note>>() {
        override fun onSuccess(data: List<Note>) {
            // Show customer notes
        }

        override fun onError(error: Throwable) {
            // Handle error
        }
})
```

| **Parameter** | **Type** | **Description**                             |
| ------------- | -------- | ------------------------------------------- |
| customerUid   | `String` | Customer UID for which to fetch the details |

**Response Field Summary**

| **Field** | **Type**     | **Description**                                              |
| --------- | ------------ | ------------------------------------------------------------ |
| data      | `List<Note>` | Response include list of `Note` which contains note content, attachment, created by and created date |