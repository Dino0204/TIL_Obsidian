## React Hook Form이란?

---

React에서 Form을 핸들링하기 위해 만들어진 라이브러리.

예를 들면 로그인, 회원가입과 같은 Form들을 효과적으로 관리할 수 있다.

  

## 설치

---

설치는 React-Router-Dom 설치처럼 간단하게 할 수 있다.

```bash
npm install react-hook-form
```

  

> **React-Hook-Form DevTools**  
>   
> Form관리를 웹페이지 내에서 효과적으로 파악 할 수 있는 툴

  

```JavaScript
npm install @hookform/devtools
```

  

## useForm

---

React-Hook-Form에서 폼 제어를 하려면 useForm이라는 Hook을 사용하면 된다.

useForm을 선언 시 반환되는 form 객체를 구조 분해 할당 문법을 사용하여 원하는 기능을 사용할 수 있는데 하나씩 살펴보도록 하겠다.

```JavaScript
import { useForm } from "react-hook-form";

const form = useForm();
```

  

## Register

---

register 함수 사용 시 객체를 또 다시 반환하게 되는데 이 때 반환되는 값을 구조 분해 할당하여 input, button등과 연결해서 사용할 수 있다.

```JavaScript
const { register } = form;
const { name, ref, onChange, onBlur } = register("email");

<input name={name} ref={ref} onChange={onChange} onBlur={onBlur}/>
```

  

### 축약형

그런데 위의 사용방식은 너무 길고 번거롭지 않은가? 그레서 React-Hook-Form 측에서는 이와 같은 간단한 방법을 제공하고 있다. 스프레드 문법을 통해 코드를 획기적으로 줄일 수 있다.

```JavaScript
const { register } = form;

<input {...register("email")}/>
```

  

## onSubmit 핸들러 제어

---

Submit 버튼을 눌렀을 때 그 후의 동작을 지정하려면 handleSubmit을 form 객체에서 구조 분해 할당을 통하여 가져온 후 원하는 동작을 할 함수를 작성하여 form 태그의 onSubmit 항목에 인자로 넣어주면 data를 확인 할 수 있다. form 데이터의 타입을 지정할 때에는 반드시 useForm에도 제네릭 타입을 지정해주자.

```JavaScript
interface FormInput {
  email: string;
  password: string;
}

const form = useForm<FormInput>();
```

```JavaScript
const { handleSubmit } = form;

const  onSubmit = (data:FormInput) => {
  console.log("Form submitted.", data)
}

<form onSubmit={handleSubmit(onSubmit)}>
	...
<form/>
```

  

## 유효성 검증

---

|유효성 검증|내용|
|---|---|
|required|필수 사항|
|minLength & maxLength|최소 & 최대 길이|
|min & max|최대 & 최소|
|pattern|패턴(정규식)|

  

form에 noValidate 옵션으로 HTML에서 기본적으로 유효성 검증하는 기능을 끌 수 있음

```JavaScript
<form onSubmit={handleSubmit(onSubmit)} noValidate>
```

  

register 함수의 두번째 인자로 유효성을 검증 할 수 있음

```JavaScript
<input
  type='email'
  {...register('email', {
	  required: "이메일은 필수로 포함되어야 합니다.",
    pattern: {
      value: /^[a-zA-Z0-9._%+-]+@gsm.hs.kr$/,
      message: "이메일 형식이 올바르지 않습니다."
    }
   }
)}/>
```

  

## useController

---

```JavaScript
function App() {
  const { control, handleSubmit, formState: { errors } } = useForm<StarRate>({
    defaultValues: {
      starRate: ""
    }
  });

  const onSubmit: SubmitHandler<StarRate> = (data) => console.log(data);

return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <RatingInput control={control} name="starRate" />
      <button type="submit">register</button>
    </form>
  );
}
```

  

```JavaScript
function RatingInput({ control, name }: any) {
  const { field } = useController({ name, control, rules: { required: true }});

  return (
    <Rating
      onChange={field.onChange}
      value={parseInt(field.value)}
      name={field.name}
    />
  );
}
```

  

```JavaScript
export interface InputField {
  id: string;
  pwd: string;
}

function ControllerInput(props: UseControllerProps<InputField>) {
  const { field } = useController(props);

  return (
    <div>
      <input {...field} placeholder={props.name} />
    </div>
  );
}
```

  

```JavaScript
function App() {
  const { control, handleSubmit } = useForm<InputField>({
    defaultValues: {
      id: "",
      pwd: "",
    },
    mode: 'onChange'
  });

  const onSubmit: SubmitHandler<InputField> = (data) => console.log(data);

	return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <ControllerInput control={control} name="id" rules={{ required: true }} />
      <ControllerInput control={control} name="pwd" rules={{ required: true }} />
      <button type="submit">login</button>
    </form>
  );
}
```

  

## 에러 메시지 표시

---

formState 객체의 errors 객체를 통해 표시함

```JavaScript
const { formState: { errors }} = form;

<p>{errors.email?.message}</p>
```

  

## React Hook Form Devtools 사용해보기

---

useForm Hook을 가져온 것 처럼 Devtool 컴포넌트를 임포트 해오면 된다.

그 다음 form을 제어하기 위해서 form 객체의 control을 Devtool의 control props로 넘겨 제어할 수 있도록 해준다. DevTool 컴포넌트 위치는 원하는 곳에 삽입 해 준다. 그러면 React-Hook-Form 로고 모양의 버튼이 하나 생기게 되는데 그 곳에서 form을 관리 할 수 있다.

  

```JavaScript
import { DevTool } from '@hookform/devtools';

const { register, control } = form;

<DevTool control={control} />
```

  

  

## 참고자료

---

[https://mycodings.fly.dev/blog/2023-09-10-all-in-one-about-react-hook-form](https://mycodings.fly.dev/blog/2023-09-10-all-in-one-about-react-hook-form)

[https://mycodings.fly.dev/blog/2023-09-11-enhanced-tutorial-of-react-hook-form#react-hook-form-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%99%84%EA%B2%B0%ED%8C%90---%EA%B3%A0%EA%B8%89%ED%8E%B8](https://mycodings.fly.dev/blog/2023-09-11-enhanced-tutorial-of-react-hook-form#react-hook-form-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%99%84%EA%B2%B0%ED%8C%90---%EA%B3%A0%EA%B8%89%ED%8E%B8)

[https://velog.io/@rjw0907/%EC%97%AC%EB%9F%AC-Form%EC%9D%84-%ED%95%98%EB%82%98%EC%9D%98-useForm-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EB%A1%9C-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-GIROK-WEB](https://velog.io/@rjw0907/%EC%97%AC%EB%9F%AC-Form%EC%9D%84-%ED%95%98%EB%82%98%EC%9D%98-useForm-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EB%A1%9C-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-GIROK-WEB)

[https://www.nextree.io/react-hook-form/](https://www.nextree.io/react-hook-form/)