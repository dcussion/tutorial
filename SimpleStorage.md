# 코드

출처: https://solidity.readthedocs.io/en/develop/introduction-to-smart-contracts.html#a-simple-smart-contract

```
pragma solidity ^0.4.0;

contract SimpleStorage {
	uint storedData;

	function set(uint x) {
		storedData = x;
	}

	function get() constant returns (uint) {
		return storedData;
	}
}
```

# 설명

SimpleStorage는 솔리디티 예제에 나와있는 가장 간단한 코드입니다. 이 코드를 이해하는 것은 어렵지 않습니다.

먼저 첫번째 줄은 이 코드가 어떤 환경에서 컴파일되어야 할지 알려줍니다. 솔리디티는 아직 개발중인 언어이고, 여러 기능의 추가와 변경이 버전 업데이트마다 이루어지기 때문에, `pragma` 키워드를 사용하여 컴파일러의 버전에 제약을 가합니다. 예를 들어 이 코드는 0.4.2 버전의 솔리디티 컴파일러에서는 컴파일이 가능하지만(0.4.2가 제약조건인 0.4.0보다 크기 때문에), 0.3.8 버전 또는 0.5.2 버전에서는 컴파일이 불가능합니다(제약조건보다 낮거나, 큰 단위의 업데이트가 이루어졌기 때문에).

두번째로, `contract Simplestorage`는 컨트랙을 정의합니다. 객체지향 프로그래밍에 익숙하다면 이것을 객체라고 생각해도 됩니다. 배포(deploy)된 컨트랙은 그 자체로 하나의 계정이며, 다른 계정과 호출을 통한 상호작용을 할 수도 있습니다. 실제로 컨트랙은 EOA(Externally Owned Account, 외부 소유 계정, 사람이 개인키로 사용하는 계정)과 마찬가지로 이더를 저장하거나 전송할 수 있습니다. 객체와 마찬가지로 컨트랙은 변수와 함수를 포함하고 있습니다.

컨트랙 내부에는 멤버 변수 `uint storedData`가 선언되어 있습니다. `uint`는 `uint256`과 같은 의미를 가지는데, 이는 0부터 2^256까지의 수를 담을 수 있는 매우 큰 타입입니다. 이 변수를 선언함으로써 컨트랙은 하나의 `uint` 값을 저장할 수 있게 됩니다. 참고로, EVM은 모든 값을 `uint256`으로 처리하기 때문에 저장 용량을 아끼기 위해 `uint8` 등의 타입을 사용하는 것은 처리 속도 면에서 비효율적입니다. 적은 값을 사용하는 경우라 하더라도 `uint` 타입을 사용하십시오.

솔리디티에서 함수를 선언하는 것은 `function` 키워드를 통해 이루어집니다. `set` 함수는 하나의 `uint` 값을 받아 `storedData` 변수에 저장합니다. `get` 함수에서 `constant`의 역할은 이 함수가 로컬에서 실행될 수 있도록 하는 것입니다. 예를 들어 `set`의 호출은 내부 변수를 수정하기 때문에 반드시 트랜잭션으로 보내져서 마이너에 의해 채굴되어야 합니다. 하지만 값의 변경이나 이더 송금 없이 내부 값을 참조하기만 하는 `get` 함수는 굳이 트랜잭션의 형태로 채굴될 필요가 없고, 그 사실을 나타내기 위해 `constant` 키워드를 붙이는 것입니다. 그리고 `set`과는 달리 이 함수가 값을 돌려준다는 사실을 나타내기 위해, `returns (uint)`를 붙입니다.

# 컨트랙

컨트랙은 Ropsten 테스트넷에 배포되었습니다: https://ropsten.etherscan.io/address/0xe9b71ba4f3fc516127830260b2be0ab19fe124d2
ABI: ```
[{"constant":false,"inputs":[{"name":"x","type":"uint256"}],"name":"set","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"get","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"}]```
[MyEtherWallet](https://www.myetherwallet.com/#contracts)에서 시험해볼 수 있습니다.
