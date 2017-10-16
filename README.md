# Introduction

Firestore is [launched](https://firebase.googleblog.com/2017/10/introducing-cloud-firestore.html) in early October 2017 to the public as a beta release. 

Google has been [recommending](https://firebase.googleblog.com/2017/10/cloud-firestore-for-rtdb-developers.html) "most new applications start with Cloud Firestore". 

However, as a developer goes through the [docs](https://firebase.google.com/docs/firestore/), you may notice there are some caveats.  

This page serves as a one-stop center to know about the things / "caveats" to consider before really adopting Cloud Firestore in an app. 

Even though Firestore addresses a number of shortcomings in the Realtime Database, it is important to note that it is not a magic silver bullet. 

# Considerations

## "Warning: Deleting a document does not delete its subcollections!"

[Link](https://firebase.google.com/docs/firestore/data-model#subcollections)

In Firestore, the data is organized in the collection -> document -> subcollection -> document -> ... structure. 

When you delete a document that has associated subcollections, the subcollections are not deleted. They are still accessible by reference.

If you want to delete documents in subcollections when deleting a document, you must do so manually, as shown in [Delete Collections](https://firebase.google.com/docs/firestore/manage-data/delete-data#collections

## Delete collection by deleting individual documents

[Link](https://firebase.google.com/docs/firestore/manage-data/delete-data)

"To delete an entire collection or subcollection in Cloud Firestore, retrieve all the documents within the collection or subcollection and delete them. If you have larger collections, you may want to delete the documents in smaller batches to avoid out-of-memory errors. Repeat the process until you've deleted the entire collection or subcollection."

## Cannot query across subcollections

[Link](https://firebase.google.com/docs/firestore/data-model#subcollections)

If you need to query data across collections, use root-level collections.

## Data nesting can be up to 100 levels deep

## Choosing data structure - nested data in document vs. subcollections vs. root-level collections

[Link](https://firebase.google.com/docs/firestore/manage-data/structure-data)

The doc explains it quite well. 

## No automatic ordering by creation date 

[Link](https://firebase.google.com/docs/firestore/manage-data/add-data)

"If you want to be able to order your documents by creation date, you should store a timestamp as a field in the documents."

## Transactions

* Read operations must come before write operations.
* A function calling a transaction (transaction function) might run more than once if a concurrent edit affects a document that the transaction reads.
* Transaction functions should not directly modify application state.
* Transactions will fail when the client is offline.

# Questions / Issues

Feel free to open an issue, or submit a pull request to update this page. 
