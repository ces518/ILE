```javascript   
   $.ajax({
        url : requestUrl,
        type : 'DELETE',
        async: true,
        data : JSON.stringify(requestParam),
        dataType : "json",
        timeout: 10000,    
        contentType:"application/json",
        
        beforeSend:function(){
            $('.wrap-loading').removeClass('display-none');
        },
        complete:function(){
            $('.wrap-loading').addClass('display-none');
        },
        success : function(data){
            if(successFunction!=undefined){
                successFunction(data);
            }
            
        },
        error : function(request,status,error){

            alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
            var err=JSON.parse(request.responseText);
            
            
            
            alert(err.resData[0].errorMsg);
            if(errorFunction!=undefined){
                errorFunction();
            }
                
            $('.wrap-loading').addClass('display-none');
        },
        fail : function() {
            alert("인터넷 연결 상태를 확인해주세요.");
            $('.wrap-loading').addClass('display-none');
        }
    });
```


*async // true , false

비동기 통신 플래그. 기본값은 true (비동기 통신)에서 요청이 던져에서 응답할 때까지 사용자 에이전트는 비동기 처리를 계속합니다. 

false로 설정 (동기 통신)하면 통신에 응답이있을 때까지 브라우저는 잠겨 조작을 받아들이지 않을 것을 주의





*contentType

서버에 데이터를 보낼 때 사용 content - type 헤더의 값입니다. 기본값은 "application / x - www - form - urlencoded"대부분의 경우이 설정으로 문제 없을 것입니다.





*dataType //The available data types are text, html, xml, json, jsonp, and script.

서버에서 반환되는 데이터 형식을 지정합니다. 생략했을 경우는, jQuery이 MIME 타입 등을 보면서 자동으로 결정합니다. 지정 가능한 값은 다음과 같은 것입니다.

"xml": XML 문서

"html": HTML을 텍스트 데이터로. 여기에 script 태그가 포함된 경우 처리가 실행됩니다.

"script": JavaScript 코드를 텍스트 데이터로. cache 옵션 특히 지정이 없으면 캐시가 자동으로 비활성화됩니다. 원격 도메인에 대한 요청의 경우 POST는 GET으로 변환됩니다.

"json": JSON 형식 데이터로 평가하고 JavaScript의 개체로 변환합니다.

"jsonp": JSONP로 요청을 부르고 callback 매개 변수에 지정된 함수 회수 값을 JSON 데이터로 처리합니다. (jQuery 1.2 추가)

"text": 일반 텍스트.





*timeOut

제한 시간 (밀리초)을 설정합니다. $. ajaxSetup 에서 지정한 값을 통신에 따라 개별적으로 덮어쓸 수 있습니다.



*type // GET, POST, DELETE, PUT


HTTP 통신의 종류를 설정합니다. 기본값은 "GET"입니다.RESTful에 "PUT"또는 "DELETE"를 지정할 수 있지만 모든 브라우저가 지원하는 것은 아니기 때문에주의가 필요



*complete

AJAX 통신 완료될 때 호출되는 함수입니다. success이나 error가 호출된 후에 호출되는 Ajax Event 입니다.




*beforeSend

AJAX에 의해 요청이 전송되기 전에 불리는 Ajax Event 입니다. 반환값을 false로 설정하면 AJAX 전송을 취소할 수 있습니다.





*error

통신에 실패했을 때 호출되는 Ajax Event 입니다.



*success

AJAX 통신이 성공하면 호출되는 Ajax Event 입니다. 돌아온 데이터와 dataType 지정한 값 2 개의 인수를받습니다.
