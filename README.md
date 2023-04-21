# Overthewrite
## Tìm hướng giải quyết và tìm offset.
- Hôm lay chúng ta lại tiếp tục giải 1 bài cơ bản về tràn biến khác :
![image](https://user-images.githubusercontent.com/130078745/233661183-6ba5a3c4-f15f-4b83-ab44-d1ef630c49b0.png)
- Nhìn sơ sơ cơ bản thì chúng ta có thể thấy đk để có thể lấy đc flag như sau:![image](https://user-images.githubusercontent.com/130078745/233661512-04b5db55-a76f-4133-b46b-43eec818521c.png)
- Khi giải bài này tui đã có 1 kinh nghiệm rằng là nên vào terminal để xem offset kỹ của từng biến , rồi mới nên bắt đầu viết tools :))).
- Sau khi đã kiểm tra địa chỉ và offset cụ thể sẽ như này: ![image](https://user-images.githubusercontent.com/130078745/233662118-09a044dc-3842-42be-9672-2fecb2ad50d7.png)
- Tuy nhiên biến V9 lại ko thể nào kiếm đc offset nên ở đây chúng ta có thể tìm bằng cách như sau:
![image](https://user-images.githubusercontent.com/130078745/233662452-b0e3f0ac-5974-434b-b244-09ada311e122.png)
![image](https://user-images.githubusercontent.com/130078745/233662776-80432670-1d21-49e4-998b-f9ca7004787d.png)
- với 0x50 = 80byte , tương đương với đó từ biến **BUF** nhập vào đến biến v9 là 80byte, nhưng khi nhập dữ liệu và kiểm tra trên terminal thì ta có thể thấy dữ liệu chỉ nhập đc 4byte là dừng .
![image](https://user-images.githubusercontent.com/130078745/233663707-1f023811-eef9-49e6-864d-9b523a91c800.png)
- Có nghĩa là offset của biến v9 là 76.
- Sau khi đã có tất cả offset thì chúng ta đã có thể tiến hành viết tools :>> .
## Thực hiện bước Viết tools bằng python.
- Với khoản cách từ biến để nhập và biến **s1** theo như offset ta tìm là 32byte.
![image](https://user-images.githubusercontent.com/130078745/233664795-9ddfbfe6-ffa9-4bf5-8ea6-e44a1b691c3f.png)
![image](https://user-images.githubusercontent.com/130078745/233664698-90ee6999-b2cd-441d-93e4-a625a0e95239.png)
![image](https://user-images.githubusercontent.com/130078745/233665327-db78a444-918e-410d-9889-dff5a8a30bcc.png)
- Thì cơ bản ta cần nhập tràn dữ liệu đến byte32 sau đấy chèn liệu là 1 chuỗi ký tự **"Welcome to KCSC"** như điều kiện đề bài cần.
![image](https://user-images.githubusercontent.com/130078745/233666207-75e89d8c-045e-4030-ab0a-382490789b00.png)
- Ta sẽ phải cộng tiếp cho 9byte để có thể nhảy đến offset của biến **V7** bỏ qua hoàn toàn biến **V6** vì đề bài ko yêu cầu gì từ nó cả.
- Nhưng ở đấy có 1 lưu ý hàm **strcmp** nó sẽ so sánh 2 chuỗi và sẽ dừng cho đến khi gặp 1 ký tự **NULL** vì thế ta ko thể tràn dữ liệu bằng ký tự **A** đc vì khi đó biến **V1** sẽ là **"Welcome to KCSCAAAAAAAAA"**. Cho nên chúng ta sử dụng **/0** để tràn dữ liệu cho hợp lí.
- Khi đã tới offset của biến **V7** (56) ta chỉ cần chèn dữ liệu vào là xong:
![image](https://user-images.githubusercontent.com/130078745/233667784-183dfe41-175f-4191-ac06-826c9a2c3e0a.png)
- offset của **V8** là 64 cho nên chúng ta ko cần phải cộng thêm bất kỳ byte nào cả, thế nên chúng ta chèn dữ liệu như sau:
![image](https://user-images.githubusercontent.com/130078745/233669188-2b9eb784-2ba5-4ed2-9ad5-1d724c07f528.png)
- Ta đã tính ra offset của biến **V9** đc rằng là 76 nhưng offset của **V8** là 64 cộng với 8 byte dữ liệu là tổng đc 72byte cho nên để có thể chèn dữ liệu cho **v9** ta cần cộng thêm 4byte và tiếp tục chèn dữ liệu cho biến **V9**.
- Ta có thể chuyển kiểu dữ liệu từ thập phân sang HEX bằng cách như sau: 
![image](https://user-images.githubusercontent.com/130078745/233669507-e0b858e8-cc0c-4621-91f0-2d5c81203ed5.png)
![image](https://user-images.githubusercontent.com/130078745/233669592-252162fe-9c4e-4b97-881c-813f1c1e366f.png)
- Sau khi chuyển ta chỉ cần nhập dữ liệu và trả dữ liệu lại cho chương trình là xong.![image](https://user-images.githubusercontent.com/130078745/233669722-cf6355ab-2f7e-4bc4-9c48-452562ce6180.png)
- Cùng chạy thử chương trình thì đã ko có lỗi nào phát sinh ra , thế là ta đã đúng và thu lại đc flag :>> .
![image](https://user-images.githubusercontent.com/130078745/233670217-7bb90727-04ae-4b9f-87c1-683c75ff2c44.png)
## KINH NGHIỆM:
- Check thật kỹ offset là đc :Đ.
