# Socket



#### Spring Boot (gradle) + React



#### Dependencies 추가

###### build.gradle

```
implementation 'org.springframework.boot:spring-boot-starter-websocket'
```



#### 서버

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

        registry.addEndpoint("/webSocket")
        		.setAllowedOrigins("*")
        		.withSockJS(); //SockJS사용
     // URL//webSocket  <-웹소켓 연결 주소

    }


    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        /**	setApplicationDestinationPrefixes()
        *	서버에서 클라이언트로부터의 메세지를 받을 api의 prefix 설정
        */       
        registry.setApplicationDestinationPrefixes("/app"); //메시지 보낼 url send /app/message
        /** enableSimpleBroker()
        *	해당 api를 구독하고 있는 클라이언트에게 메세지 전달
        */
        registry.enableSimpleBroker("/topic");	//메시지 브로커 등록  //sub용 sub topic/public
    }
}
```



controller.java

```java
import java.util.HashMap;
import java.util.Map;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.messaging.handler.annotation.MessageMapping;
import org.springframework.messaging.handler.annotation.Payload;
import org.springframework.messaging.handler.annotation.SendTo;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.hal.model.dto.Chat;
import com.hal.model.dto.ChatRequestDto;
import com.hal.model.service.ChatService;
import com.hal.model.service.RoomService;

import io.swagger.annotations.ApiOperation;

import org.springframework.messaging.simp.SimpMessageHeaderAccessor;

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
	 * 1. @SendTo를 사용하여 해당 topics를 수싲하는 client websocket에 메시지 전달
	 * 	  리턴타입 정의해야함, 리턴을 통해 client에 메시지 전달
	 * 2. SimpMessagingTemplate사용
	 *    리턴값은 void로 처리해야함
	 */
    @MessageMapping("/sendMessage/{rid}")
    @SendTo("/topic/roomId/{rid}")
    public ChatRequestDto sendMessage(@Payload ChatRequestDto chat) {
    	//메세지 db에 넣기
    	cservice.save(chat);
    	
    	// 저장 완료
        return chat;
    }

    @MessageMapping("/chat.addUser")
    @SendTo("/topic/public")
    public Chat addUser(@Payload Chat chatMessage, SimpMessageHeaderAccessor headerAccessor){
        headerAccessor.getSessionAttributes().put("username", chatMessage.getSender());
        return chatMessage;
    }
    

```



#### 클라이언트

```react

  _onMessageWasSent(message) {
    const chat = { message: '', type: '', time: new Date(), roomId: this.state.roomId, senderId: this.user.uid }

    this.websocket.current.sendMessage('/app/sendMessage/' + this.state.roomId, JSON.stringify(chat))
  }




<SockJsClient
          url={websocketUri}
          topics={topics}
          onMessage={(msg) => {
            const newMessagesCount = this.state.isOpen ? this.state.newMessagesCount : this.state.newMessagesCount + 1
            var replytext
            if (msg.type === 'text') {
              replytext = { text: msg.message }
            } else {
              replytext = { emoji: msg.message }
            }

            var tmpMessageList = this.state.totalmessageList[this.state.roomId] === undefined ? [] : this.state.totalmessageList[this.state.roomId]
            tmpMessageList.push({
              author: msg.senderId === this.user.uid ? 'me' : 'them',
              type: msg.type,
              data: replytext,
            })
          }}
          ref={this.websocket}
        />
```





###### reference

https://asfirstalways.tistory.com/359

https://github.com/lahsivjar/react-stomp/blob/HEAD/API.md

