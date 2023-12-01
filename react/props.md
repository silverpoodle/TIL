```javascript
#BEFORE
import React, { useEffect } from 'react';
import PostImage from "../atoms/postImage";
// import "../../../../../src/assets/scss/ui/organisms/postImages.scss";

function PostImages({ imageList }) {

    console.log(imageList);

    return (
        {
            imageList.map((it) => (
                < div >
                    <PostImage url={it} />
                </div >
            ))
        }
    );
}

export default PostImages;
```

#### ERROR:

causes error:Uncaught Error: Objects are not valid as a React child (found: object with keys {}). If you meant to render a collection of children, use an array instead.    at throwOnInvalidObjectType (react-dom.development.js:14887:1)

- 코드에서 문제는 `PostImages` 컴포넌트에서 `url` 프롭을 전달하는 방식
-  `PostImages` 컴포넌트에서 전체 이미지 객체를 `url` 프롭으로 전달 
  - -> `it.url`을 사용하여 URL 문자열을 얻어와야 함



```javascript
#AFTER
import React, { useEffect } from 'react';
import PostImage from "../atoms/postImage";
// import "../../../../../src/assets/scss/ui/organisms/postImages.scss";

function PostImages({ imageList }) {
    console.log(imageList);

    return (
        <div>
            {imageList.map((it) => (
                <div key={it.id}>
                    <PostImage url={it.url} />
                </div>
            ))}
        </div>
    );
}

export default PostImages;

```

1. `PostImages` 컴포넌트에서 `<PostImage url={it} />`를 `<PostImage url={it.url} />`로 변경
2. `map` 함수 내부의 래핑된 `<div>`에 `key` 프롭을 추가하여 React가 각 자식 컴포넌트를 고유하게 식별