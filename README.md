## json server(가짜서버) 사용해서 api 연결하는 작업 ✨

### 설치하기
`npm install -g json-server`
`npx json-server db.json`

### 사용하기

db.json 파일을 만든 후 아래 코드 넣어주기

```js
{
  "posts": [
    { "id": "1", "title": "a title", "views": 100 },
    { "id": "2", "title": "another title", "views": 200 }
  ],
  "comments": [
    { "id": "1", "text": "a comment about post 1", "postId": "1" },
    { "id": "2", "text": "another comment about post 1", "postId": "1" }
  ],
  "profile": {
    "name": "typicode"
  }
}
```

아래 주소로 가서 _id 의 _ 지우고 repeat 옆 숫자에 원하는 데이터 갯수 입력 후 복사   
(https://json-generator.com/)

db.json 파일에 넣어주기

```js
{
  "posts": [
    {
      "id": "1",
      "title": "a title",
      "views": 100
    },
    {
      "id": "2",
      "title": "another title",
      "views": 200
    }
  ],
  "comments": [
    {
      "id": "1",
      "text": "a comment about post 1",
      "postId": "1"
    },
    {
      "id": "2",
      "text": "another comment about post 1",
      "postId": "1"
    }
  ],
  "profile": {
    "name": "typicode"
  },
  "customer": [
    {
      "id": "65b74750123e0044c69ddeeb",
      "index": 0,
      "guid": "1fa0836b-5c7f-40b2-a98b-83f70e3f2fab",
      "isActive": true,
      "balance": "$3,859.13",
      "picture": "http://placehold.it/32x32",
      "age": 38,
      "eyeColor": "blue",
      "name": "Chrystal Boyle",
      "gender": "female",
      "company": "GEEKOSIS",
      "email": "chrystalboyle@geekosis.com",
      "phone": "+1 (948) 583-2544",
      "address": "722 Alton Place, Riegelwood, Alaska, 130",
      "about": "Ut nulla ipsum laboris laboris veniam eiusmod. Duis sint in aute sint anim aliquip ut. Ea aliquip sint incididunt do voluptate nostrud ad id ullamco nulla. Officia sint ex laboris consequat. Sint aliquip duis cillum qui Lorem occaecat in eu ullamco in sit enim laboris tempor. Reprehenderit culpa officia sunt commodo incididunt pariatur eu quis reprehenderit sit.\r\n",
      "registered": "2022-02-26T09:48:21 -09:00"
    },
```

### 데이터 가져오기
```js
 function getData() {
            fetch("http://localhost:3000/customer")
                .then((response) => response.json())
                .then((json) => {
                    const h = [];
                    for (const customer of json) {
                        h.push(`<tr>`);
                        h.push(`<td>${customer.name}</td>`);
                        h.push(`<td>${customer.company}</td>`);
                        h.push(`<td>${customer.email}</td>`);
                        h.push(`<td>${customer.address}</td>`);
                        h.push(`</tr>`);

                    }
                    document.getElementById("tbbody").innerHTML = h.join("")
                })
        }

```
### 데이터 생성하기
```js
  function postData() {
            const customer = {
                "name": "john",
                "company": "GEEKOSIS",
                "email": "john@geekosis.com",
                "phone": "+1 (948) 583-2544",
                "address": "jeju",
            };
            fetch("http://localhost:3000/customer", {
                method: "POST",
                body: JSON.stringify(customer),
                header: {
                    "content-type": "application/json; charset=UTF-8"
                },
            }).then(response => response.json())
                .then((json) => console.log(json))
        }
```

### 데이터 수정하기

fetch 주소 맨뒤에 수정 원하는 id 값을 넣어서 수정.
```js

        function putData() {
            const customer = {
                "name": "JANE",
                "company": "GEEKOSIS",
                "email": "JANE@geekosis.com",
                "phone": "+1 (948) 1111-1111",
                "address": "jeju",
            };
            fetch("http://localhost:3000/customer/c2d1", {
                method: "PUT",
                body: JSON.stringify(customer),
                header: {
                    "content-type": "application/json; charset=UTF-8"
                },
            }).then(response => response.json())
                .then((json) => console.log(json))
        }
```
### 데이터 삭제하기
fetch 주소 맨뒤에 수정 원하는 id 값을 넣어서 수정.
```js
 function deleteData() {
            const customer = {
                "name": "JANE",
                "company": "GEEKOSIS",
                "email": "JANE@geekosis.com",
                "phone": "+1 (948) 1111-1111",
                "address": "jeju",
            };
            fetch("http://localhost:3000/customer/c2d1", {
                method: "DELETE",
            }).then(response => response.json())
                .then((json) => console.log(json))
        }
```



