# Firebase DB 정리

![ㅇ](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTuawUuQCcq6fD-KpdmL4QixUOyqQqdrVNIDg&s)

<br/>

## 1. Firebase Realtime Database

- **NoSQL**
- Data structure: **Single** JSON tree
- Every time data changes, any connected device receives update
- Remain responsive even when offline
- Can be accessed directly from a mobile device or web browser (**serverless**)
- Max: 32 levels deep
  - fetches **all data of child nodes**
  - keep it flast as possible

<br/>

## 2. Firestore Database

- NoSQL

- Data structure: **Collection & Document**

  <img src="https://firebase.google.com/static/docs/firestore/images/structure-data.png" alt="dd" style="zoom:40%;" />

  <img src="https://3.bp.blogspot.com/-j9G1FSNk8gw/XQqlQGI_I3I/AAAAAAAADoI/ldmeyycIbmMbcH7-rUHX60rfNIMkDdc7gCLcBGAs/s1600/1.png" alt="d" style="zoom:67%;" />

- Every time data changes, any connected device receives update

- Can write, read, listen to, and query data even if the device is offline

  - Cloud Firestore synchronizes any local changes back to Cloud Firestore when Online

  

<br/>

<br/>

참고:

https://firebase.google.com/docs/database

https://firebase.google.com/docs/database/web/structure-data?_gl=1

https://firebase.blog/posts/2019/06/understanding-collection-group-queries/