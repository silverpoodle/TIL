```c#
using System.IO;
using System.Text;
using TMPro;
using UnityEngine;
using UnityEngine.UI;
using System.Net.Http;
using System.Threading.Tasks;
using System;

public class AITranscripts : MonoBehaviour
{
    private string apiUrl_chat = "http://localhost:8080/scenario/streaming";


    HttpClient httpClient;
    
    public Button aiTranscriptsButton;
    public TextMeshProUGUI aiTranscriptsButtonText;
    public TMP_InputField chatInputField;
    public TMP_InputField transcriptsInputField;

    bool isGeneratingBG = false;
    bool isGeneratingTS = false;

    void Start()
    {
        aiTranscriptsButton.onClick.RemoveAllListeners();
        aiTranscriptsButton.onClick.AddListener(AITranscriptsButtonEvent);

    }

//    void Update()
//    {
//        if (isGeneratingBG)
//        {
//            transcriptsInputField.text = "대본 작성 중...";
//        }
//    }

    async Task StartListeningAsync(byte[] jsonData)
    {
        using var httpClient = new HttpClient();

        var request = new HttpRequestMessage(HttpMethod.Post, apiUrl_chat);
        request.Headers.Add("Accept", "text/event-stream");
        request.Content = new ByteArrayContent(jsonData);
        request.Content.Headers.Add("Content-Type", "application/json");

        try
        {
            using var response = await httpClient.SendAsync(request, HttpCompletionOption.ResponseHeadersRead);

            if (response.IsSuccessStatusCode)
            {
                using var stream = await response.Content.ReadAsStreamAsync();
                using var reader = new StreamReader(stream, Encoding.UTF8);

                while (!reader.EndOfStream)
                {
                    string line = await reader.ReadLineAsync();

                    Debug.Log(line);

                    if (string.IsNullOrEmpty(line)) continue;

                    
                }
            }
            else
            {
                Debug.LogError($"Request failed: {response.StatusCode}");
            }
        }
        catch (Exception ex)
        {
            Debug.LogError($"Error: {ex.Message}");
        }
        finally
        {
            Debug.Log("전송 끝");
            HandleServerResponse();
        }
    }

    async void AITranscriptsButtonEvent()
    {
        string inputText = chatInputField.text;
        string json = "{\"text\":\"" + inputText + "\"}";

        aiTranscriptsButtonText.text = "작성중";
        aiTranscriptsButton.interactable = false;

        isGeneratingBG = true;
        isGeneratingTS = true;

        byte[] jsonData = Encoding.UTF8.GetBytes(json);

        try
        {
            await StartListeningAsync(jsonData);
        }
        catch (Exception ex)
        {
            Debug.LogError($"Error: {ex.Message}");
        }
    }


    void HandleServerResponse()
    {
        aiTranscriptsButtonText.text = "작성";
        aiTranscriptsButton.interactable = true;
    }

}
```





![image-20231109201836720](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20231109201836720.png)





### IMAGES

1. location

   - Home 

   - Library

   - Office 

   - Park 

   - Campus

   - Classroom



2. technique

   - 3D

   - cartoon

   - gam ecg

   - oil painting

   - painting

   - photograph



3. prompt
4. image_url





### SOUNDS

1. genre

   - ascoustic

   - children

   - chillout

   - cinematic

   - corporate

   - folk

   - hiphop
   - jazz

   - pop

   - r&b



2. mood
   - chill
   - cool
   - dramatic
   - happy
   - mysterious
   - peaceful
   - sad
   - serious



3. prompt
4. sound_url







#### 서버

- 이미지, BGM DB 구축 완료 (100%)
- 텍스트 스트리밍 AI - 서버 - 유니티 완료(100%)
  - **개행처리 확인 필요** 
- 시나리오 prompt, 결과 저장 테스트 (50%)
- 유니티 - 로그인 연동 최종 확인
  - 로그인 - 완료(100%)
  - **토큰 인증 - 진행 예정**
- 배포 설정 (80%)
  - 업데이트 시 자동배포를 위한 파이프라인 설계





```cs
using System.IO;
using System.Text;
using TMPro;
using UnityEngine;
using UnityEngine.UI;
using System.Net.Http;
using System.Threading.Tasks;
using System;

public class AITranscripts : MonoBehaviour
{
    private string apiUrl_chat = "http://metaverse.ohgiraffers.com:8080/scenario/streaming";

    public Button aiTranscriptsButton;
    public TextMeshProUGUI aiTranscriptsButtonText;
    public TMP_InputField chatInputField;
    public TMP_InputField transcriptsInputField;

    void Start()
    {
        aiTranscriptsButton.onClick.RemoveAllListeners();  //요청이 2개씩 생기는데 이유를 모르겠어서.. 썼습니다..
        aiTranscriptsButton.onClick.AddListener(AITranscriptsButtonEvent);

    }

    //    void Update()
    //    {
    //        if (isGeneratingBG)
    //        {
    //            transcriptsInputField.text = "대본 작성 중...";
    //        }
    //    }

    async Task PostJson(byte[] jsonData)
    {
        using var httpClient = new HttpClient();

        var request = new HttpRequestMessage(HttpMethod.Post, apiUrl_chat);

        //실시간 streaming 데이터 받도록
        request.Headers.Add("Accept", "text/event-stream");

        //헤더에 토큰 추가 (현재 생략 가능)
        request.Headers.Add("Authorization", 토큰);
        
        request.Content = new ByteArrayContent(jsonData);
        request.Content.Headers.Add("Content-Type", "application/json");

        try
        {
            using var response = await httpClient.SendAsync(request, HttpCompletionOption.ResponseHeadersRead);

            if (response.IsSuccessStatusCode)
            {
                using var stream = await response.Content.ReadAsStreamAsync();
                using var reader = new StreamReader(stream, Encoding.UTF8);

                while (!reader.EndOfStream)
                {
                    string line = await reader.ReadLineAsync();

                    Debug.Log(line);  //지우기

                    const string prefix = "data:";

                    if (line.StartsWith(prefix))
                    {
                        line = line.Substring(prefix.Length);
                    }

                    transcriptsInputField.text += line;

                    if (string.IsNullOrEmpty(line)) continue;


                }
            }
            else
            {
                Debug.LogError($"Request failed: {response.StatusCode}");
            }
        }
        catch (Exception ex)
        {
            Debug.LogError($"Error: {ex.Message}");
        }
        finally
        {
            Debug.Log("전송 끝");
            HandleServerResponse();
        }
    }

    async void AITranscriptsButtonEvent()
    {
        string inputText = chatInputField.text;
        string json = "{\"text\":\"" + inputText + "\"}";

        aiTranscriptsButtonText.text = "작성중";
        aiTranscriptsButton.interactable = false;

        transcriptsInputField.text = "";


        byte[] jsonData = Encoding.UTF8.GetBytes(json);

        try
        {
            await PostJson(jsonData);
        }
        catch (Exception ex)
        {
            Debug.LogError($"Error: {ex.Message}");
        }
    }


    void HandleServerResponse()
    {
        aiTranscriptsButtonText.text = "작성";
        aiTranscriptsButton.interactable = true;
    }

}


```





```java
        return webClient
                .post()
                .uri("chatbot/test_text")
                .bodyValue(bodyJson)
                .retrieve()
                .bodyToFlux(String.class)
                .map(data -> ServerSentEvent.<String>builder()
                        .data(data)
                        .build());
```





```java
Mono<String> firstResponse = Mono.just("일 \n");
        Mono<String> secondResponse = Mono.just("이 \n");
        Mono<String> thirdResponse = Mono.just("삼 \n");
        Mono<String> fourthResponse = Mono.just("사 \n");
        Mono<String> fifthResponse = Mono.just("오 ");

        Flux<ServerSentEvent<String>> responseStream = Flux.concat(
                firstResponse.map(data -> ServerSentEvent.<String>builder().data(data).build()),
                secondResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
                thirdResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
                fourthResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
                fifthResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build())
        );

        return responseStream;
```





```java
StringBuilder stringBuilder = new StringBuilder();

        return webClient
                .post()
                .uri("chatbot/test_text")
                .bodyValue(bodyJson)
                .retrieve()
                .bodyToFlux(String.class)
                .doOnNext(stringBuilder::append)
                .doOnComplete(() -> {
                    String finalString = stringBuilder.toString();
                    SaveScenarioRequest request = new SaveScenarioRequest(message, finalString);
                    scenarioCommandService.saveCreatedScenario(request);
                })
                .map(data -> ServerSentEvent.<String>builder()
                        .data(data)
                        .build());

```

 `Flux<ServerSentEvent<String>>`는 Spring WebFlux의 방식으로 이벤트 스트리밍을 처리하는데 사용

클라이언트에게 데이터를 비동기적으로 전달할 수 있게 해줌



`bodyToFlux(String.class)`를 호출하여 응답 본문을 Flux로 변환

`.map(data -> ServerSentEvent.<String>builder() .data(data) .build())`를 사용하여 각 데이터를 `ServerSentEvent`로 변g환 ->  이벤트는 클라이언트로 스트리밍되어 전송



![image-20231111230008473](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20231111230008473.png)

이미지 5장, BGM 3개 기준 10~15초 정도 걸림





```java
        List<Image> image_3D = imageRepository.findImagesByLocationAndTechnique(location, "3D");
        List<Image> image_cartoon = imageRepository.findImagesByLocationAndTechnique(location, "cartoon");
        List<Image> image_game = imageRepository.findImagesByLocationAndTechnique(location, "game cg");
        List<Image> image_oil = imageRepository.findImagesByLocationAndTechnique(location, "oil painting");
        List<Image> image_painting = imageRepository.findImagesByLocationAndTechnique(location, "painting");
        List<Image> image_photo = imageRepository.findImagesByLocationAndTechnique(location, "photograph");

        List<ImageResponse> imageResponses = new ArrayList<>();
        imageResponses.add(new ImageResponse(image_3D.get(0)));
        imageResponses.add(new ImageResponse(image_cartoon.get(0)));
        imageResponses.add(new ImageResponse(image_game.get(0)));
        imageResponses.add(new ImageResponse(image_oil.get(0)));
        imageResponses.add(new ImageResponse(image_painting.get(0)));
        imageResponses.add(new ImageResponse(image_photo.get(0)));
```



![image-20231112165644652](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20231112165644652.png)



```
2023-11-12 22:55:46.124  WARN 9108 --- [nio-8080-exec-4] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value; nested exception is com.fasterxml.jackson.databind.JsonMappingException: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value<EOL> at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 1, column: 17] (through reference chain: com.mingles.metamingle.scenario.command.application.dto.request.CreateScenarioRequest["text"])]
2023-11-12 22:55:46.125  WARN 9108 --- [nio-8080-exec-5] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value; nested exception is com.fasterxml.jackson.databind.JsonMappingException: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value<EOL> at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 1, column: 17] (through reference chain: com.mingles.metamingle.scenario.command.application.dto.request.CreateScenarioRequest["text"])]
2023-11-12 22:55:46.158  WARN 9108 --- [nio-8080-exec-6] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value; nested exception is com.fasterxml.jackson.databind.JsonMappingException: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value<EOL> at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 1, column: 17] (through reference chain: com.mingles.metamingle.scenario.command.application.dto.request.CreateScenarioRequest["text"])]
2023-11-12 22:55:46.160  WARN 9108 --- [nio-8080-exec-6] .m.m.a.ExceptionHandlerExceptionResolver : Resolved [org.springframework.web.HttpMediaTypeNotAcceptableException: Could not find acceptable representation]
2023-11-12 22:56:30.074  WARN 9108 --- [nio-8080-exec-8] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value; nested exception is com.fasterxml.jackson.databind.JsonMappingException: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value<EOL> at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 1, column: 17] (through reference chain: com.mingles.metamingle.scenario.command.application.dto.request.CreateScenarioRequest["text"])]
2023-11-12 22:56:30.075  WARN 9108 --- [nio-8080-exec-8] .m.m.a.ExceptionHandlerExceptionResolver : Resolved [org.springframework.web.HttpMediaTypeNotAcceptableException: Could not find acceptable representation]
2023-11-12 22:56:30.079  WARN 9108 --- [nio-8080-exec-7] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value; nested exception is com.fasterxml.jackson.databind.JsonMappingException: Illegal unquoted character ((CTRL-CHAR, code 10)): has to be escaped using backslash to be included in string value<EOL> at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 1, column: 17] (through reference chain: com.mingles.metamingle.scenario.command.application.dto.request.CreateScenarioRequest["text"])]
2023-11-12 22:56:30.083  WARN 9108 --- [nio-8080-exec-9] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: I
```



-> escape 문자 \n 예외처리 ***
