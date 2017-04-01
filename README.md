# Học REACT REDUX 

## Cài đặt

Nếu bạn sử dụng trên máy thì có thể sử dụng create-react-app hoặc bất kỳ react boilerplate nào bạn thích (tốt nhất là sử dụng webpack).
Bạn có thể kiểm tra dependencies đã có hay chưa.

* react
* react-dom
* redux
* react-redux

## Chuẩn bị kiến thức

Đương nhiên là bạn cần biết qua React và JavaScript (ES6)

## Giới thiệu 

Tôi viết bài này vì tôi là một tay ngang về lập trình, viết bài giúp tôi học tốt hơn nên đây chưa hẳn là lòng tốt mà viết bài cho các bạn đọc, tự sướng là chính.

Người ta luôn nói Redux cực kỳ dễ nhưng thực tế thì tôi đã học rất nhiều phen rồi mà nó cứ loạn hết cả lên, làm sao có thể nuốt nổi mấy cái khái niệm lạ lùng của Redux. Do đó, tôi cố gắng viết bài này một cách chậm rãi, tường tận nhất, diễn giải một cách dễ hiểu nhất cho ai mới bắt đầu học Redux. Có thể nói huỵch toẹt là Redux for dummies 


## Nội dung

Bài này tôi sử dụng hướng dẫn kinh điển của Redux là thực hiện một ứng dụng Todo List (học xong là làm luôn cái google keep được)

### Cơ chế của Redux

Ok, cái này đầy rẫy trên mạng, tôi chỉ note ngắn gọn vài điểm chính. Tài liệu đầy đủ nhất vẫn là tại [Redux docs](http://redux.js.org/)

**TL,DR** 

Nhắc lại một chút, bạn đã làm quen với phương thức quản lý props, state của React với chu trình LifeCycle của nó như 
*Mounting state* bằng 

- `constructor()` 
- `componentWillMount()` 
- `render()` 
-`componentDidMount()`

*Update state* bằng 

- `componentWillReceiveProps()`
- `shouldComponentUpdate()`
- `componentWillUpdate()`
- `render()`
- `componentDidUpdate()`

Destroy bằng cách *unmount* `componentWillUnmount()`

Tại sao lại nhiều quy trình vậy?! thực sự tôi chưa có điều kiện để dùng hết một đống chu trình như ở trên, tuy nhiên với cách quản lý như vậy thì khi viết một ứng dụng nó có nhiều thao tác giống nhau, hoặc hơi giống nhau, bạn sẽ nhận ra rằng mình đang gặp rắc rối về quản lý state như thế nào. Vì vậy, không phải lúc nào cũng dùng React hoặc nhất thiết phải dùng Redux để quản lý state, cái đó phụ thuộc vào cái bạn đang làm, nhưng tốt nhất nên biết cả hai (một số bạn có thể tìm hiểu và sử dụng MobX thay cho Redux, ok, đường nào cũng tới Paris).

**Khái niệm Redux** 

Cá nhân tôi nhìn nhận một chương trình JavaScript về mặt cơ bản là tập hợp các object và nó biến đổi liên tục trong quá trình chạy chương trình thông qua các phương thức hay function mà bản thân phương thức hay function cũng là object. Vì vậy, theo như tôi hiểu thì các nhà thiết kế của facebook đã nhìn nhận dưới một góc nhìn cơ bản nhất của chương trình để tạo ra Redux. 

1. Redux quan niệm các state chỉ đơn thuần là một plain object, ví dụ app Todo nó là một object sau:

```js
{
	todos: [{
		id: 0,
		text: 'Ăn cơm',
		completed: true
	}, {
		id: 1,
		text: 'Uống nước',
		complete: false
	}],
	visibilityFilter: 'SHOW_COMPLETED'
}
```
Ở ví dụ này bạn thấy có 2 state chính là `todos` và `visibilityFilter` 

Trong `todos` ta lại có 2 nội dung `todos.text` và `todos.completed`, đây gọi nôm na là *actions* trong ứng dụng.

2. Để thay đổi các state `todos.text` và `todos.completed` đó, bạn phải dispatch actions,*action* này cũng là plain object luôn:

```js
{
	type: 'ADD_TODO',
	text: 'Ăn cơm'	
}
```
```js
{
	type: 'SET_VISIBILITY_FILTER',
	filter: 'SHOW_COMPLED' 
}
```
Lưu ý là `type` là tên gọi của action bắt buộc theo quy định của Redux, còn `text` hay `filter` được gọi chung là `payload`, bạn đặt nó là gì thì tuỳ vào cái mình đang làm. 

3. Để kết nối state với action thì cần có reducer, vai trò của reducer là lưu 

```js
let initialState = []; // tạo một state mặc định
const todos = (state = initialState, action) => {
	switch (action.type) {
		case 'ADD_TODO': 
			return [
				...state,
				{
					id: action.id,
					text: action.text,
					completed: false 
				}
			];
		default: 
			return state;
	}
};

```
Bạn có thể viết thêm reducer khác để quản lý các reducer.

**Ba nguyên tắc Redux**

1.	Single source of truth 

Toàn bộ state của ứng dụng được lưu trữ trong một cây object tại một store duy nhất. Lý thuyết này nhằm giúp giới hạn sự trùng lặp dữ liệu và liên kết dữ liệu giữa các đối tượng khác nhau. 

2. State is read-only 

Cách duy nhất để thay đổi state là đưa ra một action -- một object mô tả hoạt động

3. Sự thay đổi được tạo bởi pure function

Pure function là function chỉ return giá trị được tạo bởi chính tham số của function. ví dụ 
```js
function square(x) {
	return x * x;
}

function squareAll(items) {
	return items.map(square);
}

```

**Quy trình Redux** 

Các khái niệm sơ bộ thì chúng ta nắm rồi, nhưng tôi tóm lại quy trình ở đây.

Step 1. User tạo một action (là một object).
Step 2. Các action đó được reducer nhận diện và so sánh với action mẫu. Action và reducer được lưu trữ trong store.  
Step 3. Sau khi reducer nhận diện, nó sẽ dispatch action đó từ store để hiển thị trên giao diện. 

## Bài tập 

Với bài tập, tôi sử dụng [JS Bin](http://jsbin.com/) nên có hơi khác một chút so với 

* [Phần 1: Bắt đầu từ Mock Up](/p1.md)
* [Phần 2: Tạo Reducer](/p2.md)
* [Phần 3: Kết hợp các reducer lại với nhau](/p3.md)
* [Phần 4: Kết hợp với React component](/p4.md)
* [Phần 5: Tách các Component](/p5.md)
