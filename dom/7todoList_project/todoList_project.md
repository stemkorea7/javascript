새로운 vscode 창 띄우기  
index.html & app.js & style.css 파일 생성

.html
title변경
구글폰트 접속, Lora 폰트 검색 후 선택 링크복사 (구글이 무료로 제공하는 폰트를 사용가능)
cdnjs font awesome 검색 후 asset Type에서 스타일링 선택 후 첫번째 링크 복사 
(font awsome은 무료로 아이콘을 만들수 있다. 사용법은 헤더에 링크를 걸고
font awsome 접속해보면 icons라는 메뉴를 클릭해보면 사용할 수 있는 아이콘들이 뜨는데 
아무 아이콘을 클릭하고 start using font awesome 을 클릭해보면 클래스 이름을 제공한다.
style.css 링크
app.js 링크

<header> <h1> Todo List </h1> </header>
form > 
input .input
button .todo-button >
i .fas fa-plus-square

div .todo-container >
ul .todo-list > 이안에 자바스크립트 코드를 활용해서 li태그와 삭제 버튼과 체크버튼을 생성할 예정
div .todo >
li태그
삭제와 체크 버튼

day2
스타일링 
전체범위에 해당
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-image: url("https://images.pexels.com/photos/247421/pexels-photo-247421.jpeg?cs=srgb&dl=pexels-pixabay-247421.jpg&fm=jpg");
  color: #ffffff;
  font-family: "Lora";
  /* min-height: 100vh; */
}

header {
  font-size: 1.5rem;
}

header,
form {
  min-height: 20vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

form input,
form button {
  padding: 0.5rem;
  font-size: 2rem;
  border: none;
  background-color: white;
}

form button {
  color: teal;
  background: white;
  cursor: pointer;
  transition: all 0.3s ease;
}

form button:hover {
  background: teal;
  color: white;
}

day3
이번엔 셀렉터와 이벤트 리스너 함수를 차례대로 만들어 볼 예정
//셀렉터
const todoInput = document.querySelector(".todo-input");
const todoButton = document.querySelector(".todo-button");
const todoList = document.querySelector(".todo-list");

//이벤트 리스너
todoButton.addEventListener("click", addTodo);

//함수
function addTodo(e) {
  e.preventDefault();
  console.log("hello"); 접근을 확인하기 위해 콘솔
}

그리고 우리는 투두리스트 생성 버튼을 눌렀을때 아래와 같은 코드들이 여러개 생성될 수 있도록
    <div class="todo-container">
        <ul class="todo-list">
            <li></li>
            <button></button>
        </ul>
    </div>

//함수
function addTodo(e) {
  e.preventDefault();
  console.log("hello");
//div 생성
  const todoDiv = document.createElement("div");
  todoDiv.classList.add("todo");
 //li 태그 생성
  const newTodo = document.createElement("li");
  newTodo.classList.add("todo-item");
  newTodo.innerText = "test";
  todoDiv.appendChild(newTodo);
  //체크버튼
  const checkButton = document.createElement("button");
  checkButton.classList.add("check-btn");
  checkButton.innerHTML = '<i class="fas fa-check"> </i>';
  todoDiv.appendChild(checkButton);
 

여기서 체크버튼은 font awesome에 있는 아이콘을 사용할 예정인데
 innerText 명령어는 값을 문자열로 인식하기 때문에 아이태그를 생성할 수 없다.
이럴땐 innerText 대신 innerHTML을 사용한다.

삭제버튼은 체크버튼을 그대로 복사해서 이름만 조금 수정한다.
 //삭제버튼
  const deleteButton = document.createElement("button");
  deleteButton.classList.add("delete-btn");
  deleteButton.innerHTML = '<i class="fas fa-trash"> </i>';
  todoDiv.appendChild(deleteButton);

마지막으로 여태까지 생성했던 모든 내용들을 ul태그인 todoList에 todoDiv를 추가한다.
여기까지 완료하면 추가하기 버튼을 누를때마다 아래와같이 ul태그안에 html 코드가 생성되는 것이다.
  <div class="todoDiv">
                <li class="todo-item">
                </li>
                <button class="check-btn"><i class="fas fa-check"></i></button>
                <button class="delete-btn"><i class="fasfa-trash"></i></button>
            </div>

그리고 확인해 보면 추가할때마다 정리가 안된 버튼이 생성되는것을 볼 수 있다. 다음시간에는
이내용들을 꾸미도록 하겠다.

day4
체크버튼과 삭제버튼 디자인

style.css
.todo-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo-list {
  min-width: 30%;
  list-style: none;
}

.todo {
  margin: 0.5rem;
  background: white;
  color: black;
  font-size: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.todo li {
  flex: 1;
}

.delete-btn,
.check-btn {
  background: coral;
  color: white;
  border: none;
  padding: 1rem;
  font-size: 1rem;
}

.check-btn {
  background: teal;
}

app.js
const input = document.querySelector(".input"); html에 있는 인풋 클래스 선택
newTodo 생성하는 newTodo.innerText = input.value; 로 변경 그리고 input.value = ""; 빈공간으로 초기화

style.css
.todo-item 패딩 0.5 추가
.todo-item {
  padding: 0.5rem;
}

day5
리스너 추가
.js
todoList.addEventListener("click", deleteCheckFn);


function deleteCheckFn(e) {
  const item = e.target;
  if (item.classList[0] === "delete-btn") {
// item.remove(); 그냥 타겟을 삭제하면 삭제버튼만 삭제된다. 그래서 아래와 같이 부모엘리먼트까지
선택해서 모두 삭제해준다.
    const todo = item.parentElement;
    todo.remove();
  }
삭제버튼을 눌러보다보면 가끔 삭제가 안될때가 있다. 이유를 알기위해 console.log(item); 으로 찍어본다
삭제가 안될땐 i태그가 뜨고 삭제가 될땐 button 태그가 뜨는걸 알 수 있다. 그래서 선택도구로 자세히
살펴보면 i태그가 z축 즉, 맨위에 있고 그밑에 button태그가 깔려있는것을 알 수 있다. 
그래서 i태그에 가려져 버튼이 클릭이 안돼 삭제함수가 실행되지 않는다.
우리는 이때 css로 i태그가 클릭이 안되게할 수 있는데 명령어는

style.css 
font awesome에서 제공하는 아이콘들을 무시하자.
.fa-trash,
.fa-check {
  pointer-events: none;
}
확인

그리고 이번엔 체크버튼의 기능을 만들어보자
app.js
  if (item.classList[0] === "check-btn") {
    const todo = item.parentElement;
    todo.classList.toggle("checkIt"); 토글로 checkIt 클래스를 만들어서
  }
}

.css
텍스트에 줄을 긋고, 불투명하게 만들어준다.
.checkIt {
  text-decoration: line-through;
  opacity: 0.5;
}
그리고 div 부모 .todo 클래스에  transition: all 0.5s ease; 추가

day6
Animations (skip.)

day7
Filtering

.html
html옵션을 form안에 넣어줌
 
    <div class="select">
        <select name="todos" class="filter">
            <option value="all">All</option>
            <option value="checked">Checked</option>
            <option value="unChecked">UnChecked</option>
        </select>
    </div>

select 스타일링

select {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  outline: none;
  border: none;
  color: teal;
  width: 10rem;
  cursor: pointer;
  padding: 1rem;
}

.select {
  margin: 1rem;
  position: relative;
  overflow: hidden;
}

.select::after {
  content: "\25BC";
  position: absolute;
  background: teal;
  top: 0;
  right: 0;
  padding: 1rem;
  pointer-events: none;
}

app.js
const filterOption = document.querySelector(".filter");
셀렉트 클래스 filter 선택

filterOption.addEventListener("click", filterTodo);
이벤트 리스너 추가

function filterTodo(e) {}
filterTodo 함수 생성


function filterTodo(e) {
  const todos = todoList.childNodes;
필터링을 위해 차일드 노드 생성 / 콘솔로 todos 확인

  for (todo of todos) {
    switch (e.target.value) {
      case "all":
        todo.style.display = "flex";
        console.log("all");
        break;
여기서 case의 all은 html Option의 all value이다. all은 모두 표시기때문에 조건없이 flex

      case "checked":
        if (todo.classList.contains("checkIt")) {
          todo.style.display = "flex";
          console.log("checked");
        } else {
          todo.style.display = "none";
        }
        break;

case checked value일 경우 
모든 것 중 토글 checkIt 클래스가 포함되어 있는 것들만 모두 flex 아니면 none
checkIt이 포함되어 있는지 알기위해 (todo.classList.contains("checkIt") 조건을 줌

      case "unChecked":
        if (!todo.classList.contains("checkIt")) {
          todo.style.display = "flex";
          console.log("unchecked");
        } else {
          todo.style.display = "none";
        }
    }
  }
}
