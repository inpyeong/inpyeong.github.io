---
layout: single
title: "crpytography_symmetric_key"
---

## Symmetric encryption
대칭 암호화는 하나의 비밀키가 암호화와 복호화에 모두 사용되는 암호화 알고리즘 형태 중 하나로, conventional / private-key / single-key 등으로 불립니다. 발송자와 수령자는 공통의 키를 공유하게 됩니다. 

![No Image](/assets/images/symmetric-encryption.png)

대칭 암호화에서는 보안을 위해 __두 가지 요구사항__ 이 있습니다.
* 강력한 암호화 알고리즘
* 오직 sender와 receiver만 알고 있는 비밀키
  
그리고 미리 __가정해야 할 사항__ 은 다음과 같습니다.
* sender와 receiver는 사용된 암호화 알고리즘이 무엇인지 알고 있다.
* 키를 공유할 보안 채널이 있다.

## One time pad
One time pad란, __메시지 m과 같은 크기를 갖는 랜덤 암호키__ 와 메시지 m을 XOR 연산을 통해 encryption, decryption을 하는 것을 뜻합니다. 여기서 사용되는 랜덤 암호키는 메시지 송신자와 수신자 둘에게만 공유되며, 메시지를 전송할 때마다 매번 바뀌어야 합니다.

### 결정적인 약점
One time pad의 결정적인 약점은 바로 메세지의 크기와 암호키의 크기가 같다는 특징에서 발견할 수 있습니다. 만약 메시지의 크기가 1GB라면 암호키의 크기 또한 1GB여야 하는데 이는 너무 비효율적이라 할 수 있습니다. 그리고 안전한 암호키의 공유 또한 힘들기 때문에 이 또한 약점으로도 볼 수 있습니다.

따라서 One time pad는 기밀성(confidentiality)에 대해서 굉장히 완벽한 방법이지만, 현실적으로 쓰이진 않고 있습니다.

## Symmetric key
대칭 키 암호화에는 두 가지 방법이 존재합니다.
* __Block cipher__: 정보를 정해진 블록 단위로 암호화한다.
  * DES, AES
* __Streaming cipher__: 유사난수를 연속적으로 생성하여 암호화하려는 자료와 결합하여 암호화한다.
  * RC4

\
그럼 지금부터 각 암호 방식들에 대해 알아보도록 할까요..?

## Block cipher
앞서 언급했듯이 Symmetric key의 Block cipher는 암호화할 정보를 정해진 블록 단위로 나누어 암호화하는 암호를 말합니다. Block cipher에 속하는 암호 알고리즘은 대표적으로 DES, AES가 있습니다.

### DES
DES란 Data Encryption Standard의 약자로, symmetric key의 __Block cipher__ 알고리즘 중 하나입니다. IBM에서 고안되어 NIST가 미국 표준 암호 알고리즘으로 채택되었으며, 예전에는 많이 사용되었지만 오늘날 컴퓨터로 쉽게 해독이 가능하기 때문에 이제는 사용할 수 없게 되었습니다.

사용하는 암호키의 크기는 64bit입니다. 이 중에서 8bit는 parity check로 사용하기 때문에 사실상 암호키의 크기는 __56bit__ 로 생각하면 됩니다.

\
Block Cipher이기 때문에 동작 원리는 다음과 같습니다.
1. 암호화할 메시지 m을 여러 개의 64bit 블럭으로 나눈다.
2. 블럭 단위로 암호화를 실시하는데, 마지막 블럭이 64bit보다 작은 경우 padding을 붙여서 64bit로 만든 후 암호화를 진행한다.

\
![No Image](/assets/images/des.png){: width="400px" height="400px"}{: .center}

위 그림을 보면서 DES의 원리에 대해 간략히 설명하겠습니다.
1. 암호화할 메시지를 64bit로 쪼갠다.
   * 쪼개진 것들을 블럭이라고 부른다. 그림에서는 '64-bit input'이 한 블럭이라 보면 된다.
2. permutation 과정을 통해 비트 간의 순서를 바꾼다.
   * permutation 과정을 확대한 이미지는 아래와 같습니다.
     \
     \
     ![No Image](/assets/images/des-permutation.png){: width="85%"}
3. 64bit 블럭을 32bit로 나눈 후, 56bit key로부터 생성한 48bit 랜덤넘버(K)와 암호화를 실시한다.
   * '64-bit input'를 32bit로 나누고 순서를 바꾸며 Mangler 함수를 쓰는 이러한 구조를 Feistel cipher 라고 한다.
4. 16개의 round동안 이를 반복한다.

\
위에서 나온 용어들에 대해 아래서 다시 설명하겠습니다.

### DES round



