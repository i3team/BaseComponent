# BaseInput
Tất cả các component cho chức năng nhập text ... như I3TextField hoặc EHealthTextField nên kế thừa lại từ component BaseInput. Component này có chức năng tạo debounce để giảm thiểu độ giật lag khi type.
### Các điều cần lưu ý:
1. Các component kế thừa lại từ BaseInput thì value truyền vào cho <input /> hay các component cho chức năng tương đương phải lấy từ this.state.value, props onChange truyền cho phải là this.onChange(). 
2. Khi trả về cho onChange bên ngoài parameter khác e (synthetist event) thì override lại hàm proccessEventToOnChange pararameter đầy vào là e (synthetist event) và phải return về một giá trị bất kì mà bạn muốn.
3. Ở một số trường hợp shông muốn sử dụng chức năng debounce thì truyền props debounce giá trị là 0;
4. Phải override lại hàm consumerContent tương tự như BaseConsumer
5. Hiện tại parameter e đang trẻ về là một object được extend từ e (synthetist event) của React gồm 2 trường là target và which. Nếu muốn lấy thêm thì truyền props eventFields là một mảng string các field cần lấy.
### Props
Name | Type | Default | Description
:--- | :--- | :--- | :---
`debounce` | bool | true | `onChange` được invoke sau khi dừng nhập một khoảng (350ms)
`onChange`| func | | Khác với `onChange` của input thông thường, `onChange` của Searchbox có parameter là text, không phải event
`eventFields` | array of string | | Thêm các trường để lấy cho event trả về
### Ví dụ
```jsx
 Class ExampleTextField extends BaseInput {
    //Muốn trả về giá trị khác e thì override hàm này
    proccessEventToOnChange(e) {
        return e;
    }
    proccessEventToOnChange(e) {
        return e.target.data;
    }
    consumerContent(){
        return (
            <input 
                value={this.state.value}
                onChange={this.onChange}
                eventFields={["key","code"]}
            />
        )
    }
 }
 ```
