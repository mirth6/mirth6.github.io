# Web Socket

[TOC]



### Web Socket이란?

- 내가 원하는 정보에 대해 구독을 신청하고, 토픽에 대한 메세지를 발행하면 해당 토픽을 구독하고 있는 모든 사용자에게 보내주는 방식

| Web Socket                                          | HTTP/HTTPS                                      |
| --------------------------------------------------- | ----------------------------------------------- |
| 서버에 요청을 보내지 않아도 서버가 정보를 줌        | 클라이언트가 요청 했을 때 서버가 해당 정보 응답 |
| 한번 연결하면 연결이 유지됨                         | 매번 연결을 요청해야함                          |
| ws<br />wss : 데이터 보안을 위해 ssl적용<br />topic | http<br />https<br />uri                        |

### STOMP



### 코드

환경: Spring Boot (gradle) + React

#### 서버

###### build.gradle

```
implementation 'org.springframework.boot:spring-boot-starter-websocket'
```



###### WebSocketConfig.java

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.messaging.simp.config.MessageBrokerRegistry;
import org.springframework.web.socket.config.annotation.EnableWebSocketMessageBroker;
import org.springframework.web.socket.config.annotation.StompEndpointRegistry;
import org.springframework.web.socket.config.annotation.WebSocketMessageBrokerConfigurer;

@Configuration
@EnableWebSocketMessageBroker//@EnableWebSocketMessageBroker is used to enable our WebSocket server
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        /* addEndpoint()
        *	연결할 소켓 엔드포인트를 지정
        *	서버 base url뒤에 붙음
        */
        registry.addEndpoint("/webSocket")
        		.setAllowedOrigins("*")
        		.withSockJS(); //SockJS사용
    }

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        /* setApplicationDestinationPrefixes()
        *	도착 경로에 대한 prefix설정
        *	서버에서 클라이언트로부터의 메세지를 받을 api의 prefix 설정
        */       
        registry.setApplicationDestinationPrefixes("/app");
        /* enableSimpleBroker()
        *	메세지 브로커 등록
        *	해당 api를 구독하고 있는 클라이언트에게 메세지 전달
        *	/topic : 구독한 n명에게 메세지를 뿌려야 하는 경우
        *	/queue : 메세지를 발행한 한명에게 다시 정보를 보내는 경우
        */
        registry.enableSimpleBroker("/topic","/queue");	//메시지 브로커 등록  //sub용 sub topic/public
    }
}
```



###### controller.java

```java

import org.springframework.messaging.handler.annotation.MessageMapping;
import org.springframework.messaging.handler.annotation.Payload;
import org.springframework.messaging.handler.annotation.SendTo;

import org.springframework.messaging.simp.SimpMessageHeaderAccessor;

import com.hal.model.dto.ChatRequestDto;
/** ChatRequestDto
*/

@CrossOrigin(origins = {"*"}, maxAge = 6000)
@RestController
@RequestMapping("/chats")
public class ChatController {
	/**
	 * 이벤트 trigger방식(2가지)
	 * 1. client소켓에서 sendMessage함수로 메시지 보낼경우 @MessageMapping으로 받을 수 있음
	 * 2. GET사용할때는 @RequestMapping 사용
	 * 
	 * 메시지 응답방식(2가지)
	 * 1. @SendTo('/topic')
	 *		1:n으로 메세지 뿌릴때
	 *		해당 topics를 수싲하는 client websocket에 메시지 전달
	 * 	  	리턴타입 정의해야함, 리턴을 통해 client에 메시지 전달
	 *	  @SendToUser('/queue')
	 *		1:1로 메세지 보낼때
	 * 2. SimpMessagingTemplate사용
	 *    리턴값은 void로 처리해야함
	 */
    @MessageMapping("/sendMessage/{rid}")
    @SendTo("/topic/roomId/{rid}")
    public ChatRequestDto sendMessage(@Payload ChatRequestDto chat) {
    	//메세지 db에 넣기
    	cservice.save(chat);

        return chat;
    }

    @MessageMapping("/chat.addUser")
    @SendTo("/topic/public")
    public Chat addUser(@Payload Chat chatMessage, SimpMessageHeaderAccessor headerAccessor){
        headerAccessor.getSessionAttributes().put("username", chatMessage.getSender());
        return chatMessage;
    }
    
}
```



#### 클라이언트

```
install react-stomp
```

###### ChatList.jsx

```react
import React from 'react'
import { ListView } from '@progress/kendo-react-listview'
import API, { websocketUri } from '../apis/api'
import ChatItem from '../components/Chat/ChatItem'
import ChatWindow from '../components/Chat/ChatWindow'
import SockJsClient from 'react-stomp'

class ChatList extends React.Component {
  user = JSON.parse(sessionStorage.getItem('user') || '{}')

  constructor(props) {
    super(props)
    this.state = {
    }
    this.websocket = React.createRef()
  }

  // 메세지 전송 버튼을 눌렀을때 실행되는 함수
  _onMessageWasSent(message) {
    const chat = { message: '전달할 메세지', time: new Date(), roomId: '채팅방id', senderId: this.user.uid }

    /* sendMessage(주소,보낼 메세지)
    *  주소:
    *	controller에 @MessageMapping에 매핑 되있는 주소
    *  보낼 메세지:
    *	controller에 @Payload로 받는 객체 형식이랑 맞추기
    */
    this.websocket.current.sendMessage('/app/sendMessage/' + '채팅방id', JSON.stringify(chat))
  }

  render() {
    return (
      <div>
        <SockJsClient
            /*
            *  url={}
            *  topics={}
            *  onMessage{(msg)=>{}}
            */
          url={websocketUri}	
            //websocketUri: 'https://localhost:8080/api/webSocket'
          topics={'/topic/roomId/채팅방id'} 
            //{['/topic/roomId/1','/topic/roomId/2']} 처럼 여러개도 가능
          onMessage={(msg) => {
                    //msg는 서버에서 return해준 객체
                    //받은거 실행
          }}
          ref={this.websocket}
        />

        <ChatWindow
          messageList={this.state.totalmessageList[this.state.roomId]}
          onUserInputSubmit={this._onMessageWasSent.bind(this)} //메세지 전송
          onFilesSelected={this.props.onFilesSelected}
          agentProfile={{
            teamName: this.state.receiver.name,
            imageUrl: this.state.receiver.profileImg,
          }}
          isOpen={this.state.isOpen}
          onClose={this.handleClick.bind(this)}
          showEmoji={true}
        />

      </div>
    )
  }
}

export default ChatList

```





###### reference

https://hyeooona825.tistory.com/89

https://asfirstalways.tistory.com/359

\<SockJsClient> props

https://github.com/lahsivjar/react-stomp/blob/HEAD/API.md

