
# TCP 흐름제어
* REC (Retransmission Error Control) 재전송 기반 에러제어    
* ARQ (Automatic Repeat Request) 자동 재전송 요구   
* Stop and Wait : 매번 전송한 패킷에 대해 확인 응답을 받아야만 그 다음 패킷을 전송하는 방법   
* Sliding Window (Go Back N ARQ)   
=>수신측에서 설정한 윈도우 크기만큼 송신측에서 확인응답없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 제어기법   
=>NAK를 받은 이후의 데이터를 모두 다시 보낸다. 중복문제.   
* Selective ARQ   
=> NAK를 받은 송신측은 에러 발생한 프레임만 전송   
* Adaptive ARQ    
=> 통신회선 상태에 따라 블록 사이즈를 조절하여 전송   


# TCP 혼잡제어
* AIMD(Additive Increase / Multiplicative Decrease)   
=> 처음엔 패킷 하나씩 보냄. 문제없으면 Window 크기를 1씩 증가시켜가며 보냄   
=> 패킷전송에 실패하거나 타임아웃 넘기면 속도를 절반으로 줄임   
=> 나중에 진입하는 쪽이 처음엔 불리하지만, 시간이 지나면 평행상태로 수렴   
=> 초기에 낮은 대역폭으로 오랜 시간이 걸리고 혼잡상황 미리 캐치하지 못함. 혼잡 발생하고 나서야 대역폭 줄임   

* Slow Start (느린 시작)    
=> AIMD 방식은 처음에 전송 속도가 늦다   
=> Slow Start 방식은 AIMD와 마찬가지로 패킷 하나씩 보내며 시작하고 문제없으면 ACK 패킷마다 windowSize를 1씩 늘린다. 즉 한주기마다 windowsize가 2배   
=> AIMD에 반해 전송속도가 지수함수 꼴로 증가. 혼잡현상 발생하면 window size 1로 떨어뜨린다.   
=> 처음에는 수용량을 예상못하지만 혼잡 발생하고 나면 어느정도 수용량 예상 가능   
=> 따라서, 혼잡 발생했던 윈도우 사이즈의 절반까지는 지수함수꼴로 윈도우 크기 증가시키고 그 이후로는 완만하게 1씩 증가   

* Fast Retransmit (빠른 재전송)    
=> 중복된 순번 패킷 3개 받으면 재전송 받게되면 혼잡을 감지하고 윈도우 사이즈 줄인다.   

* fast Recovery (빠른 회복)   
=> 혼잡 상태가 되면 윈도우 사이즈를 1로 줄이지 않고 반으로 줄이고 선형증가   
=> 혼잡 한번 겪고 부터는 AIMD 방식으로 동작


## Tahoe 와 Reno   
### Slow Start Threshold(ssthresh)를 뜻하는 것으로, 여기까지만 Slow Start를 사용하겠다   
* Tahoe나 Reno와 같은 정책들은 AIMD와 Slow Start를 적절히 섞어서 사용   

* Tahoe   
=> 처음에는 Slow Start-> 윈도우 크기 지수 증가 -> ssthresh -> AIMD 선형적 윈도우 증가 -> Ack Duplicate or TimeOut -> ssthresh ,윈도우 크기 수정 -> Slow Start   

* Reno    
=>처음에는 Slow Start-> 윈도우 크기 지수 증가 -> ssthresh -> AIMD 선형적 윈도우 증가 -> Ack Duplicate -> fast Recovery   
=>                                                                               -> TimeOut -> Slow Start   


