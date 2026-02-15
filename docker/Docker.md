# Docker

## Container
컨테이너란 OS 위에 만들어지는 '격리'된 가상 환경

### Why Container?
1\. Compare with VM(Virtual Machine)

VM은 Hypervisor 위에 OS까지 가상화하여 격리한다.  
다만, Docker는 Host OS 커널을 공유하면서 사용자 공간만 격리하여 실행한다.  
따라서 가볍고 더 빠르게 애플리케이션을 실행할 수 있다.

2\. Use MSA(Micro Service Architecture) in company

정확히는 컨테이너가 MSA 운영을 쉽게 만들어줘서 MSA를 선택하는 회사가 많아졌지만,  
신입 개발자 입장에서는 반대로 회사가 많이 채택하니까 공부해서 나쁠 것 없다!라고 이해하면 될 것 같다.

