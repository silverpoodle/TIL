# **📝 Synchronous**



<img src="https://jujubebat.github.io/assets/images/2020-09-01-19-59-27.png" alt="img" style="zoom: 80%;" />

<img src="/Users/jungin/Library/Application Support/typora-user-images/image-20240208140902510.png" alt="image-20240208140902510" style="zoom:40%;" />



## **📌 핵심요약**

**동기식 모델은 호출된 함수의 수행 결과 및 종료를 호출한 함수가 처리**

## **📌 설명**

- Synchronous의 뜻은 무엇일까? 네이버에 검색해보면 “동시 발생[존재]하는”라고 나와있습니다.
- Synchronous는 Sync(함께)와 Chrono(시간)가 결합된 단어입니다.
- “시간을 함께 맞춘다.” 대충 이런 의미로 생각해볼 수 있습니다. 누가 어떤 시간을 맞춘다는 것일까요?
- 먼저 동기식 모델이 어떻게 동작하는지 알아봅시다.
  - 동기식 모델에서 A함수에서 B함수를 호출하는 상황을 가정해봅시다.
    1. B 함수의 작업 완료는 A함수가 최종적으로 처리합니다.
    2. 즉, A함수는 B함수를 호출하고 B함수의 수행 결과 및 종료를 처리합니다.
       - B함수가 완료될 때까지 대기하다가 처리할 수도 있고(블로킹 동기)
       - B함수가 완료될 때까지 다른 작업을 수행하면서, B작업의 완료 여부를 계속 체크하다가 처리할 수도 있습니다. (논블로킹 동기)
- 요약 하자면, 동기식에서는 작업을 요청한 함수가 작업 완료를 계속 확인하며 신경을 씁니다.
- 동기식 모델에서는 작업이 순차적으로 진행됩니다.
- 위에서 살펴본 상황에서 A함수는 B함수의  완료를 직접 처리하고나서 다음 작업을 수행할 것입니다.
- B함수가 완료될 때까지 다른 작업을 수행하기도 한다며? (논블로킹 동기)
- 이는 B함수의 작업이 완료되었는지 체크하는 와중에 다른 작업을 할 수 있다는 뜻입니다.
- 크게보면 어쨌든 B함수의 작업이 완료 되어야지 A함수는 다른 작업을 수행할 수 있습니다. (아래코드 참조)

```c
Future ft = asyncFileChannel.read(~~~);

while(!ft.isDone()) {
    // isDone()은 asyncChannle.read() 작업이 완료되지 않았다면 false를 바로 리턴해준다.
    // isDone()은 물어보면 대답을 해줄 뿐 작업 완료를 스스로 신경쓰지 않고,
    // isDone()을 호출하는 쪽에서 계속 isDone()을 호출하면서 작업 완료를 신경쓴다.
    // asyncChannle.read()이 완료되지 않아도 여기에서 다른 작업 수행 가능 
}

// 작업이 완료되면 작업 결과에 따른 다른 작업 처리
```

- 다시, 누가 어떤 시간을 맞춘다는 것일까요?(동기라고 부르는 이유는 무엇일까?)라는 질문으로 돌아가봅시다.
  - B함수의 실행과 그것에 대한 결과가 한 타이밍에 이루어진다고 해석할 수 있습니다. (B함수를 실행하고 그 결과를 받을때까지 기다리니까)
  - A함수가 B함수를 호출했으면, B함수의 결과는 (시간이 얼마나 걸리더라도) 그 자리에서 받습니다.
  - 즉, 작업의 요청과 결과가 같은 시점에 일어나기 때문에 **동기**라고 부르는 것입니다.



# **📝 ASynchronous**



<img src="https://jujubebat.github.io/assets/images/2020-09-01-20-00-51.png" alt="img" style="zoom: 80%;" />

<img src="/Users/jungin/Library/Application Support/typora-user-images/image-20240208141201448.png" alt="image-20240208141201448" style="zoom:40%;" />



## **📌 핵심요약**

**비동기식(ASynchronous) 모델은 호출된 함수의 수행 결과 및 종료를 호출된 함수가 처리하는 것입니다.**

## **📌 설명**

- 부정관사 A가 붙어있는 ASynchronous는 비동기라는 뜻입니다.

- 비동기식 모델이 어떻게 동작하는지 알아봅시다.

  - 비동기식 모델에서 A함수에서 B함수를 호출하는 상황을 가정해봅시다.
    1. B함수의 작업 완료는 B함수가 직접 혼자 처리합니다.
    2. 즉 B함수는 스스로 수행 결과 및 종료를 처리합니다.
    3. B함수는 작업 수행을 완료하면 그 결과를 A함수에게 알릴 뿐입니다.
    4. A함수는 B함수의 작업 완료를 신경쓰지 않기 때문에 B함수를 호출한 후 다른 작업을 수행할 수 있습니다.

- 요약하자면, 작업을 요청한 함수가 작업 완료 여부를 신경쓰지 않고 자기 할일을 한다면, 비동기입니다.

- 비동기식 모델에서는 작업이 순차적으로 진행되는 것을 보장할 수 없습니다.

- 위에서 살펴본 상황에서 A함수는 B함수의 완료 여부에 상관없이 작업을 수행합니다.

- B함수가 끝나지 않았는데도 A함수는 다른 작업을 수행할 수 있으므로

  작업이 순차적으로 수행되지 않을 수 있습니다.

- 비동기라고 부르는 이유는 동기라고 부르는 이유의 반대라고 생각하면 됩니다.

  - 비동기식 모델에서 B함수의 실행과 결과는 한 타이밍에 이루어지지 않습니다.
  - B함수를 호출하고, A함수가 다른 작업을 다 끝내고, B함수가 완료될 수도 있습니다.
  - 즉, 작업의 요청과 결과가 동시에 이루어지지 않기 때문에 **비동기**라고 부르는 것입니다..





# **📝 Blocking I/O**

<img src="https://jujubebat.github.io/assets/images/2020-09-01-22-36-48.png" alt="img" style="zoom: 80%;" />

## **📌 핵심 요약**

**블로킹(Blocking)이란 호출된 함수가 자신이 할 일을 모두 마칠 때까지 제어권을 계속 가지고 있고, 그 동안 호출한 함수는 대기 하는 것을 말합니다.**

## **📌 설명**

- blocking이란 작업의 멈춤, 대기(wait)를 뜻하는 단어입니다. 어떤 상황에서 누가 blocking이 된다는 것일까요?

  - 블로킹 방식에서 A함수에서 B함수를 호출하는 상황을 가정해봅시다.
    1. A함수는 B함수를 호출하면서 제어권을 넘겨줍니다.
    2. B함수는 제어권을 넘겨 받고, 자신의 작업을 완료하기 전까지 제어권을 돌려주지 않습니다.
    3. A함수는 B함수가 완료될 때까지 제어권을 돌려받지 못하므로 아무것도 못합니다. 즉, 대기상태, block 상태입니다.
    4. B함수가 완료되면 제어권을 A함수에게 return 합니다.
    5. 제어권을 다시 돌려받은 A함수는 그 다음 작업을 수행합니다.

- 다시 한 번 정리해보자면, Blocking이란 호출된 함수가 자신의 작업을 모두 마칠때까지 호출한 함수에게 제어권을 주지 않고 대기하게 만드는 것입니다.

- 위 그림을 보면 프로세스는 커널을 통해 I/O 작업(Read)을 합니다.

- 프로세스는 I/O 작업을 위한 시스템콜 호출 이후

  I/O 기기에서 datagram을 읽어올 때까지 프로세스는 blocking 되는 것을 볼 수 있습니다.





# **📝 Non-Blocking**

<img src="https://jujubebat.github.io/assets/images/2020-09-01-22-50-44.png" alt="img" style="zoom: 80%;" />



## **📌 핵심 요약**

**논블로킹(Non-Blocking)이란 호출된 함수의 작업 완료 여부에 상관없이 제어권을 호출한 함수한테 바로 리턴하여, 호출한 함수가 다른 작업을 할 수 있는 것을 말합니다.**

## **📌 설명**

- non-blocking이란 말그대로 블로킹이 안된다는 것이다. 어떤 상황에서 누가 non-blocking 된다는 것일까요?

  - 논블로킹 방식하에서 A함수에서 B함수를 호출하는 상황을 가정해봅시다.

    1. A함수는 B함수를 호출하면서 제어권을 넘겨줍니다.
    2. B함수는 제어권을 넘겨받고, 자신의 작업 완료 여부에 상관없이

    제어권을 곧장 A함수에게 다시 넘겨줍니다.

    1. A함수는 제어권을 곧장 돌려받고, 다른 작업을 수행할 수 있습니다.(B함수의 완료와 상관없이)
    2. B함수의 작업이 완료되면, 그 결과를 A함수에게 통지한다.

  - 다시 한 번 정리 해보자면, Non-Blocking이란 호출된 함수의 작업 완료 여부에 상관 없이, 호출한 함수는 제어권을 곧장 돌려받고, 다른 작업을 수행할 수 있는 것입니다.

- 위 그림을 보면 프로세스는 커널을 통해 I/O 작업(Read)을 합니다.

- 프로세스는 I/O 작업을 위한 시스템콜을 호출합니다.

- 하지만 I/O 기기에서 데이터를 읽기전에(No datagram ready)

  EWOULDBLOCK을 리턴 받습니다. (EWOULDBLOCK는 아직 작업이 진행 중이란 뜻입니다.)

- 즉, I/O 작업이 완료되지 않았음에도 불구하고 제어권을 곧장 돌려받아

  프로세스는 block되지 않는 것입니다. (block되지 않는 동안 다른 작업 수행 가능.)







# **📝 Synchronous, ASynchronous, Blocking, Non-Blocking**

<img src="https://blog.kakaocdn.net/dn/tNK78/btrg0pQ5rkU/ORaGjkXvIE3qD0eIVIeVSk/img.png" alt="Blocking or Non-Blocking, Synchronous and Asynchronous" style="zoom:50%;" />

<img src="https://cdn.inflearn.com/public/comments/08f0d98d-5a36-4701-880e-e3ca0189d2a3/%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5.png" alt="추가적인 Blocking / Non-Blocking" style="zoom:25%;" />



- 블락, 논블락, 동기, 비동기가 각각 쌍을 이루어 4가지 조합이 만들어집니다.



## **📌 Synchronous-Blocking**

<img src="/Users/jungin/Library/Application Support/typora-user-images/image-20240208144919168.png" alt="image-20240208144919168" style="zoom:40%;" />

<img src="https://velog.velcdn.com/images%2Fnittre%2Fpost%2F8cdc0a02-d469-47d5-96c8-f6aeef204eb7%2Fimage.png" alt="img" style="zoom:67%;" />





## **📌 Asynchronous-Non-Blocking**

<img src="http://i.imgur.com/iSafBIF.png" alt="Imgur" style="zoom:40%;" />

<img src="https://velog.velcdn.com/images%2Fnittre%2Fpost%2Fb9566928-9a6b-4111-9cad-528daa45475d%2Fimage.png" alt="img" style="zoom:77%;" />



## **📌 Synchronous-Non-Blocking**

<img src="http://i.imgur.com/a8xZ9No.png" alt="Imgur" style="zoom:45%;" />

<img src="https://velog.velcdn.com/images%2Fnittre%2Fpost%2Ffe5d1231-4c3c-4caf-bdd8-2287926e38ca%2Fimage.png" alt="img" style="zoom:67%;" />





## **📌 ASynchronous-Blocking**

<img src="http://i.imgur.com/zKF0CgK.png" alt="Imgur" style="zoom:45%;" />

<img src="https://velog.velcdn.com/images%2Fnittre%2Fpost%2F9b6754f0-8721-4308-8a62-d884c7315d15%2Fimage.png" alt="img" style="zoom:67%;" />