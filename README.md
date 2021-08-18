# 숫자야구
#### 프로젝트 기간 - 2021.05.25 - 2021.05.28
#### 프로젝트 팀원 - [Joey](https://github.com/joey-ful), [EHD](https://github.com/Brian2931)

## Step1

### 🤓 학습 내용 / 핵심 경험
#### 프로젝트 설계
- FlowChart 만들어보기
- 함수 구현사항 미리 설계해보기

#### Swift
- 함수 단위 최소화 하기
- 코드의 depth 최소화하기
- Optional에 익숙해지기
- Swift 컨벤션 익히기

#### Git
- 첫 페어 프로그래밍 경험해보기
- Git의 커밋 단위, 커밋 메시지 형식, 브랜칭 전략 고민하기


### 🖼 플로우차트

<img src="https://user-images.githubusercontent.com/52592748/119810997-91732300-bf21-11eb-8ef4-b81eead1eb68.png" width="500">

### 📝 함수 설계

#### 0. 전역 변수

- answer: Int
- trialNumber: Int
- userWin: Bool
- gameEnd: Bool

#### 1. `playGameRound()` - 메인 함수

- `generateRandomArray()`을 호출해 사용자값 받기
- gameEnd가 false인 동안 `proceedGameRound()`로 게임 진행
- 게임이 진행될 때마다 trialNumber를 1 감소해서 남은 횟수 업데이트

#### 2. `checkExitConditions(userValue:)` - 사용자 승리여부와 게임 종료 여부를 결정하는 함수

#### 3. `showResult(userValue:userWin:gameEnd:)` - 결과 출력 함수

- "임의의 수: 숫자 숫자 숫자" 출력
- 사용자 승패 여부에 따라 관련 메시지를 출력하는 `printWinner()` 호출
- 게임 진행 상황 출력
    - 스트라이크, 볼
    - 남은 기회

#### 4. `printWinner()` - 누구의 승리인지 출력하는 함수

#### 5. `generateRandomArray()` - 랜덤한 정답 생성 함수

- 중복없는 랜덤한 수를 3개 생성
- 생성한 수를 배열에 넣어서 리턴
    - e.g. [8, 2, 4]

#### 6. `getStrikeCount(userValue:)` - Strike 개수 출력 함수

- zip() 함수와 filter() 고차함수를 활용

#### 7. `getBallCount()` - Ball 개수 출력 함수

- 정답과 사용자 입력값을 Set으로 묶어 개수를 확인 => 중복이 있다면 개수가 줄어드는 것을 확인해 볼 개수 체크

<details>
<summary> <b> :page_facing_up: 함수 설계 1차 시도 </b>  </summary>
<div markdown="1">

#### 0. 게임 옵션 함수 `chooseOption()`

- 1.게임시작, 2.게임종료 출력
- 게임시작한다면 옵션번호 입력받기
    - 1: 게임시작 ⇒ `1. 게임 시작 함수` 호출
    - 2: 게임종료⇒ `return 0`
    - 그 외는 `0. 게임 옵션 함수` 재실행

#### 1. 게임 시작 함수 `playGame()`

- `2. 정답 생성 함수` 호출 ⇒ let answer = generateAnswer()
- 시도횟수 변수 선언(초깃값 = 9) trialNumber = 9

```swift
let trialNo = 9

while trialNo > 0 {
    let userInput = getUserInput()

    if compareAnswer(userInput) == 1 {
        didWin()
        chooseOption()
        return
    }
    trailNo -= 1
}

didWin()
chooseOption()
```

- `3. 사용자 입력값 받는 함수` 호출 ⇒ let userInput = getUserInput()
- `5. 정답이 맞는지 확인하는 함수` 호출

#### 2. 정답 생성 함수 `generateAnswer()`

- 랜덤한 수를 3개 생성
- 그 수들을 배열에 넣어서 리턴
    - [8, 2, 4]

#### 3. 사용자 입력값 받는 함수 `getUserInput()`

- `readLine()`으로 입력 받기
- `4. 예외처리 하는 함수`를 호출
    - -1이 리턴되면 다시 입력값 받기 ⇒ `2번 함수 재실행` 혹은 while문
    - 1이 리턴되면 사용자 입력값을 배열에 넣어서 리턴 ⇒ `return [Int(input[0]), Int(input[2]), Int(input[4])]`

#### 4. 예외처리 하는 함수 `checkError()`

- 에러 발생하는 경우
    - 문자열 길이가 5가 아닌 경우
    - `input[0]`, `input[2]`, `input[4]`이 1~9가 아닌 경우
    - `input[1]`, `input[3]` 이 공백이 아닌 경우
    - `input[0]`, `input[2]`, `input[4]`에 중복이 있는 경우
- 리턴값
    - 에러가 발생하면 -1을 리턴
    - 에러가 없으면 1을 리턴

#### 5. 정답이 맞는지 확인하는 함수 `compareAnswer()`

- 인자: 정답배열, 사용자입력값배열
- strikeCount = 스트라이크 확인 함수 호출
- ballCount = 볼 확인 함수 호출
- print("`스트라이크 \(strikeCount), 볼 \(ballCount - strikeCount)`")
- 리턴
    - strikeCount == 3면 리턴 1
    - else 리턴 -1

#### 6. trialNo를 통해 승리여부 확인 `didWin()`

```jsx
if tiralNo = 0 {
    print("컴퓨터승리")
} else {
    print("사용자승리")
}
```
</div>
</details>
<br><br>
