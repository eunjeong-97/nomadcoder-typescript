# TypeScript 설정

> #### 목차

- [TypeScript 설정](#typescript-설정)
  - [1. TypeScript 설치](#1-typescript-설치)
    - [추가적인 패키지 설치](#추가적인-패키지-설치)
      - [`tsc-watch`](#tsc-watch)
      - [`crypto-js`](#crypto-js)
  - [2. root 폴더에 `tsconfig.json` 파일생성](#2-root-폴더에-tsconfigjson-파일생성)
      - [tsc-watch 패키지 적용 전](#tsc-watch-패키지-적용-전)
      - [tsc-watch 패키지 적용한 상태](#tsc-watch-패키지-적용한-상태)
    - [`include`](#include)
    - [`exclude`](#exclude)
  - [3. Ts -> Js 컴파일](#3-ts---js-컴파일)
    - [`package.json` 명령어 설정](#packagejson-명령어-설정)
  - [4. TypeScript 연습1](#4-typescript-연습1)
    - [`export {};`](#export-)
    - [선택적인 parameter](#선택적인-parameter)
  - [5. TypeScript 타입](#5-typescript-타입)
    - [`void`](#void)
  - [6. TypeScript의 `인터페이스`](#6-typescript의-인터페이스)
    - [클래스](#클래스)
      - [JavaScript에서의 클래스](#javascript에서의-클래스)
      - [TypeScript에서의 클래스](#typescript에서의-클래스)
      - [`class Human {}`](#class-human-)
      - [`constructor()`](#constructor)
  - [7. Block 생성](#7-block-생성)

## 1. TypeScript 설치

```
$ yarn global add typescript
```

### 추가적인 패키지 설치

#### `tsc-watch`

1. `tsc-watch` 패키지 설치

```
$ yarn add tsc-watch --dev
```

2. `package.json` 명령어 수정

```json
"scripts": {
  "start": "tsc-watch --onSuccess \"node dist/index.js\" ",
  "prestart": "tsc"
  },
```

- `yarn start` 명령어를 입력할 때마다 새로고침되도록 설정
- `tsc-watch` 가 `--onSuccess` 라면 `command`를 불러온다 
- `\"node dist/index.js\"`

3. `src` 폴더 및 `dist` 폴더 생성

4. `tsconfig.json` 수정

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES2015",
    "sourceMap": true,
    "outDir": "dist"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

- 내 모든 TypeScript 파일들을 `src` 폴더 안에 들어가고
- 모든 컴파일된 파일들은 `dist` 폴더 안에 들어갈 것이다

5. `.gitignore` 파일에 추가

```
node_modules
.env
dist
```

6. `yarn start` 명령어 실행

- `watch모드` 에서 컴파일을 한다
- `watch모드` : src폴더에서 무언가를 바꿀 때마다 dist내용이 변경된다


#### `crypto-js`

## 2. root 폴더에 `tsconfig.json` 파일생성

- TypeScript 파일이 어떻게 JavaScript로 변환되는지 알려준다
- 옵션설정

#### tsc-watch 패키지 적용 전

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES2015",
    "sourceMap": true,
  },
  "include": ["index.ts"],
  "exclude": ["node_modules"]
}
```

#### tsc-watch 패키지 적용한 상태

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES2015",
    "sourceMap": true,
    "outDir": "dist"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

### `include`

- 어떤 파일들이 컴파일 과정에 포함될 파일을 `array` 형태로 적으면 된다
- ts 파일을 적어주면 된다
- 여기서는 src 폴더 안에 있는 모든 것들을 컴파일한다고 설정했다

### `exclude`

- 컴파일할 때 제외할 파일
- 디폴트로 `node_modules` 폴더는 컴파일하지 않는다고 설정하면 된다

## 3. Ts -> Js 컴파일

- ts파일에 있는 코드를 컴파일해서 `index.js` 와 `index.js.map` 을 만든다

```
$ tsc
```

### `package.json` 명령어 설정

```json
"scripts": {
  "start": "node index.js",
  "prestart": "tsc"
  },
```

- `yarn start` 명령어를 할 때 `index.js` 파일을 실행하는데
- 이러한 `index.js` 파일은 `index.ts` 파일을 컴파일 해서 생성하는 것이기 때문에
- `prestart` 명령어로 `tsc` 로, TypeScript를 먼저 컴파일해준다
- 따라서 `yarn start` 명령어를 입력하게 되면, yarn은 prestart 를 먼저 실행하고 start를 실행한다

## 4. TypeScript 연습1

```ts
const name = 'Nico',
age = 24,
gender = 'male';

const sayHi = (name, age, gender) => {
  console.log(`Hello ${name}, you are ${age}, and your gender is ${gender}.` );
}

satHi(name, age, gender);

export {};
```

- 이렇게 코드를 작성하고 터미널에서 `yarn start` 명령어를 입력하면 콘솔창에 `Hello Nico, you are 24, and your gender is male.` 나올 것이다
- `satHi(name, age);` 라고 적는다면, 3개의 arguments를 예상했는데 내가 2개만 적었다고 에러를 보여준다.

### `export {};`

- TypeScript 법칙
- 해당 파일이 모듈로 된다는 걸 이해할 수 있도록 가장 하단에 적어준다
- 만약 이걸 하지 않는다면, 내가 이름을 선언할 수 없다고 에러메시지가 발생할 것이다.

### 선택적인 parameter

```ts
const sayHi = (name, age, gender?) => {
  console.log(`Hello ${name}, you are ${age}, and your gender is ${gender}.` );
}

satHi(name, age);
```

- 이렇게 `parameter` 뒤에 `?` 를 입력하게 되면 선택적인 것으로 되는데
- `undefined` 로 나온다

## 5. TypeScript 타입

```ts
const sayHi = (name:string, age:number, gender?:string):void => {
  console.log(`Hello ${name}, you are ${age}, and your gender is ${gender}.` );
}

sayHi("Nico", 24, "male");
```

만약 큰 function을 만들 때 많은 인수 `arguments` 를 넣을텐데
어떤 인수 `arguments` 를 줘야할지 잊을 수도 있다.

### `void`

- sayHi의 function 들이 어떤 유형의 값을 돌려주는지 나타내기 위해 parameter 뒤에 위치시킨다
- 하지만 여기서는 `console.log()` 만 실행하기 때문에 리턴값을 주지 않을 것이다
- 따라서 리턴값의 유형을 `void` 라고 지정한다
- sayHi function에서 아무런 값도 나오지 않도록 한다

- 만약 return값을 주는 상태에서 `void` 로 설정하려고 하면 안된다고 에러가 발생할 것이다.

## 6. TypeScript의 `인터페이스`

내가 `object` 를 사용하고 싶다면,
typescript가 object를 이해할 수 있게 하고
그 object가 올바른 type인지 아닌지 분별하게끔 해야한다.

function에 object를 전달할 때 그 function은 전달받은 object로 무언가를 할 것이다.

```ts
interface Human {
  name: string;
  gender: string;
  age: number;
}

const person = {
  name: 'Nico',
  gender: 'male',
  age: 24
}

const sayHi = (person:Human):string => {
  return `Hello ${person.name}, you are ${person.age}, and your gender is ${person.gender}.`;
}

console.log(sayHi(person));

export {};
```

- argument를 하나씩 따로 parsing 하는 것보다는 
- 위와 같이 `Human을 원함` 또는 `person을 원함` 같이 자유롭게 설정하고, 
- 타입은 `Human`으로 설정한다  
- TypeScript는 `person`이 `Human 인터페이스`와 동일한 구조를 가지고 있는데 체크한다
- JavaScript에서는 작동하지 않는다 `only TypeScript`

> 인터페이스의 활용

- 블럭체인의 경우, 하나의 `block`을 인터페이스로 할 수 있다
- 그 블럭이 가져야되는 모든 세부 설명

### 클래스

- 인터페이스는 JavaScript로 컴파일되지 않는다.
- 하지만 가끔 인터페이스를 JavaScript에 넣고 싶을 때가 있을텐데
- 이럴 때 사용할 수 있는 것이 `클래스` 이다
- 코드를 컨트롤 할 수 있게 해준다

#### JavaScript에서의 클래스

- 클래스의 속성 `property` 들을 묘사할 필요가 없다
- 클래스를 만들고 클래스가 어떤 속성을 가져야 하는지 선언할 필요가 없다

#### TypeScript에서의 클래스

- 하지만 TypeScript에서는 클래스가 어떤 속성 `property` 을 가지는지, 
- 그런 속성들이 가지고 있는 권한 `permission`에 대해 선언해야 한다


```ts
class Human {
  public name = string;
  public age = number;
  public gender = string;
  constructor(name:string, age:number, gender?:string) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
}

const lynn = new Human('Lynn', '18');

const sayHi = (person:Human):string => {
  return `Hello ${person.name}, you are ${person.age}, and your gender is ${person.gender}.`;
}

console.log(sayHi(lynn));

```

#### `class Human {}`

- name이라는 이름의 public 속성을 선언한다
- 자바스크립트에서 `public`이나 `private` 속성에 차별을 두지 않는다

#### `constructor()`

- 클래스가 시작할 때마다 호출되는 함수이다.
- 즉, 클래스로부터 객체 `object` 를 만들 때마다
- 같은 속성의 이름을 argument로 준다
- `this.name = name;` : 이 클래스의 name은 생성자의 name과 동일하다

이번에는 `index.js` 파일로 가면 클래스를 확인할 수 있다
그래서 인터페이스가 필요할 때와 클래스가 필요할 때가 있을 것이다.
왜냐하면 js코드가 인터페이스를 사용하게 되면 ts측면에서 좀 더 안전하다
하지만 react, express, node 같은 라이브러리를 사용한다면 클래스를 사용해야 할 것이다
public 속성의 변수 `variable` 들은 나타나지 않는다

> private 속성

```ts
class Human {
  private name = string;
  private age = number;
  private gender = string;
  constructor(name:string, age:number, gender?:string) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
}

const lynn = new Human('Lynn', '18');

const sayHi = (person:Human):string => {
  return `Hello ${person.name}, you are ${person.age}, and your gender is ${person.gender}.`;
}

console.log(sayHi(lynn));
```

`sayHi()` 내부에서 `person.name`, `person.age`, `person.gender` 를 부르게 되면
private 속성으로 생성된 property들은 Human 클래스 내부에서만 접근이 가능하다고 에러가 발생한다
`person.age`를 Human 클래스 밖에서 부르기 때문에 TS에서는 컴파일하지 않는다

이와같이 TypeScript는 내가 변경을 원하는지의 여부에 따라서  코드들을 보호해주면서 사용할 수 없다.

## 7. Block 생성

> 0.7 강 이어서