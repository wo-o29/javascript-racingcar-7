## 🏁 과제 진행 요구 사항

<details>
<summary>자세히 보기</summary>

<br/>

- 미션은 과제를 포크하고 클론하는 것으로 시작한다.

- 기능을 구현하기 전 `README.md` 에 구현 할 기능 목록을 정리하여 추가한다.
- Git의 커밋 단위는 앞 단계에서 `README.md`에 정리한 기능 목록 단위로 추가한다.

</details>

## ⚙️ 기능 요구 사항

<details>
<summary>자세히 보기</summary>

<br/>

> **초간단 자동차 경주 게임을 구현한다.**

- 주어진 횟수 동안 n대의 자동차는 `전진` 또는 `멈출 수` 있다.

- 각 자동차에 이름을 부여할 수 있다. 전진하는 자동차를 출력할 때 이름을 같이 출력한다.
- 각 자동차에 이름은 `쉼표(,)`를 기준으로 구분하며 `이름은 5자이하만 가능`하다.
- 사용자는 몇 번의 이동을 할 것인지 입력할 수 있어야 한다.
- 전진하는 조건은 `0에서 9 사이에서 무작위 값`을 구한 후 그 값이 `4 이상`일 경우이다.
- 게임을 완료한 후 누가 우승했는지 알려준다. 우승자는 `한 명 이상`일 수 있다.
  - 우승자가 `여러 명일 경우 쉼표(,)를 이용`하여 구분한다.
- 사용자가 잘못된 값을 입력할 경우 `[ERROR]` 로 시작하는 메세지와 함께 `Error`를 발생시킨 후 애플리케이션은 종료되어야 한다.

### 📸 입출력 요구 사항

**[입력]**

- 경주할 자동차 이름(이름은 쉼표(,) 기준으로 구분)
- 시도할 횟수

**[출력]**

- 차수별 실행 결과
- 단독 우승자 안내 문구
- 공동 우승자 안내 문구

**실행 결과 예시**

```tsx
경주할 자동차 이름을 입력하세요.(이름은 쉼표(,) 기준으로 구분)
pobi,woni,jun
시도할 횟수는 몇 회인가요?
5

실행 결과
pobi : -
woni :
jun : -

pobi : --
woni : -
jun : --

pobi : ---
woni : --
jun : ---

pobi : ----
woni : ---
jun : ----

pobi : -----
woni : ----
jun : -----

최종 우승자 : pobi, jun
```

</details>

## 💻 프로그래밍 요구 사항 1

<details>
<summary>자세히 보기</summary>
<br/>

- Node.js 20.17.0 버전에서 실행 가능해야 한다.

- 프로그램 실행의 시작점은 `App.js` 의 `run()` 이다.
- `package.json` 은 변경할 수 없으며, 제공된 라이브러리만 사용해야 한다.
- 프로그램 종료 시 `process.exit()`를 호출하지 않는다.
- 프로그래밍 요구 사항에서 달리 명시하지 않는 한 파일, 패키지 등의 이름을 바꾸거나 이동하지 않는다.
- 자바스크립트 코드 컨벤션을 지키면서 코드를 작성한다.

</details>

## 💻 프로그래밍 요구 사항 2

<details>
<summary>자세히 보기</summary>
<br/>

- depth는 2까지만 허용한다.

  - while문안에 if문이 있다면 depth는 2이다.

  - 조건과 분기를 위한 인덴트가 2depth가 넘지 않는 것을 의미한다.
  - 단순히 가독성을 위해 depth가 깊어지는 경우는 작성 가능하다.

- 삼항 연산자는 사용하지 않는다.
- 함수가 한 가지 일만 하도록 최대한 작게 만들기
- Jest를 이용하여 정리한 기능 목록이 정상적으로 작동하는지 테스트한다.

</details>

## 🤔 생각해보기

<details>
<summary>자세히 보기</summary>

### 가설 1. 자동차 이름에 중복을 허용할지?

→ **전진할 때는 입력한 순서로 구분할 수 있지만, 최종 결과에서 자동차의 이름만 출력하기 때문에 어떤 자동차가 우승했는지 알 수 없기 때문에 중복 금지**

### 가설 2. 자동차 이름에 공백은 어떻게 처리할지?

`1. 모든 공백 허용`, `2. 모든 공백 제거(앞, 뒤, 중간)`, `3. 앞, 뒤 공백만 제거`

- 문자열 중간에 있는 공백은 유저가 확인하기 쉽고 의도적으로 입력된 경우가 많을 것 같다.
- 하지만 앞, 뒤 공백은 실수로 입력되는 경우가 많은 것 같아서 제거해주면 좋을 것 같다.

→ **`앞, 뒤 공백만 제거`**

### 가설 3. 자동차 이름에 빈 문자열이 오는 경우

→ **예외 처리 하기, `최소 1자 이상 5자 이하로 제한`**

### 가설 4. 시도할 횟수에 음수나 소수가 오는 경우

→ **양의 정수 이외의 값은 모두 예외 처리하기**

</details>

## 📝 코드 설계

<details>
<summary>자세히 보기</summary>
<br/>

1. 자동차 이름들을 입력 받는다.

2. 자동차 이름들을 `쉼표(,)` 를 기준으로 나눈다.
3. 각 자동차 이름에 `앞, 뒤 공백을 제거`한다.
4. 자동차 이름들에 `중복이 있다면` 예외 처리한다.
5. 자동차 이름이 `1자 이상 5자 이하가 아닌 경우` 예외 처리한다.
6. 시도할 횟수를 입력 받는다.
7. `양의 정수가 아니라면` 예외 처리한다.
8. 시도할 횟수 만큼 전진하고 결과를 출력한다.
9. 결과를 보고 최종 우승자를 구한다.
10. 최종 우승자를 출력한다.

</details>

## 🎯 구현 할 기능 목록

<details open>
<summary>자세히 보기</summary>
<br/>

- [x] 자동차 이름들을 입력 받는다.
  - [x] 자동차 이름들을 `쉼표(,)` 를 기준으로 나눈다.
  - [x] 각 자동차 이름에 `앞, 뒤 공백을 제거`한다.
- [x] 자동차 이름들에 `중복이 있다면` 예외 처리한다.
- [x] 자동차 이름이 `1자 이상 5자 이하가 아닌 경우` 예외 처리한다.
- [x] 시도할 횟수를 입력 받는다.
- [ ] `양의 정수가 아니라면` 예외 처리한다.
- [ ] 시도할 횟수 만큼 전진하고 결과를 출력한다.
- [ ] 마지막 결과를 기준으로 최종 우승자를 구한다.
- [ ] 최종 우승자를 출력한다.

</details>
