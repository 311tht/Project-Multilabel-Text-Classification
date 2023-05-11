# Project-Multilabel-Text-Classification
## Phần I: Mô tả project
Multilabel Text Classification là một bài toán trong Machine Learning liên quan đến việc phân loại văn bản trên nhiều class khác nhau. Với bài phân loại văn bản cơ bản, một mẫu dữ liệu sẽ được gán nhãn chỉ bằng 1 class duy nhất (Multiclass Text Classification). Tuy nhiên với trường hợp của Multilabel, một văn bản sẽ được gán nhãn với n class (n là số class của bài toán) thông qua việc gán giá trị 0, 1 (tương ứng với có hoặc không có) với từng vị trí của class trong nhãn.

Như vậy, Input/Output của bài toán sẽ là: 
- Input: Một đoạn văn bản (string).
- Output: Vector n phần tử (gồm các số thực có giá trị thuộc khoảng (0, 1)).

Ở project này, sẽ giải quyết một bài toán về Multilabel Text Classification thông qua bài Multilabel Sentiment Analysis. Trong đó, nhiệm vụ là cần dự đoán các nhãn có trong một dòng Tweet.

## Phần II: Cài đặt chương trình
Trong phần này, xây dựng một mô hình Multilabel Text Classification cơ bản bằng Tensorflow sử dụng một số mạng nơ-ron đã học ở bài trước. Tổng quan về toàn bộ quy trình của project sẽ thực hiện theo như hình dưới đây:

### Chuẩn hóa dữ liệu: 
Để giảm bớt độ phức tạp của các dòng Tweet, ta sẽ thực hiện chuẩn hóa dữ liệu sử dụng một vài các phương pháp chuẩn hóa dữ liệu văn bản. Các phương pháp được áp dụng trong project bao gồm:
- Chuyển chữ viết thường (Lowercasing). • Unidecode.
- Xóa dấu câu (Punctuation Removal).
- Xóa stopwords (Stopwords Removal).
- Stemming.

### Xây dựng mô hình: 
Xây dựng mô hình theo kiến trúc được mô tả như sau (danh sách dưới đây mô tả theo thứ tự trong tf.keras.Sequential):
- Embedding Layer: Từ vector output của text vectorization layer, ta đưa vào layer embed-ding. Chức năng chính của layer này là để biểu diễn các phần tử số nguyên trong vector đầu vào thành các vector với cùng chiều dài (embedding dims).
- BiLSTM Layer 1: Từ vector output của embedding layer, ta đưa vào layer BiLSTM đầu tiên với 64 units. Lưu ý rằng cần phải trả về vector output của toàn bộ timestep tại layer này để có thể làm input của layer BiLSTM tiếp theo.
- BiLSTM Layer 2: Layer BiLSTM thứ 2 với 64 units, trả về hidden state của toàn bộ timestep.
- BiLSTM Layer 3: Layer BiLSTM cuối cùng với 64 units, với layer này ta sẽ chỉ trả về vector output tại timestep cuối cùng.
- Dropout Layer 1: Layer Dropout với tỉ lệ drop = 0.2.
- Fully-connected Layer 1: Từ vector output của RNN layer cuối cùng, ta đưa vào một lớp
fully-connected layer thứ nhất với 64 node với activation function là ’relu’.
- Dropout Layer 2: Layer Dropout với tỉ lệ drop = 0.3.
- Fully-connected Layer 2: Lớp fully-connected layer thứ hai với 32 node với activation function là ’relu’.
- Dropout Layer 3: Layer Dropout với tỉ lệ drop = 0.3.
- Output Layer: Fully-connected layer với 11 nodes (tượng trưng cho 11 class) và activation function là ’sigmoid’.

## Phần 3: Kết luận
Có thể thấy, kết quả mà mô hình xây dựng chưa thật sự tốt. Thật vậy, đây là một bài toán có độ phức tạp và thách thức lớn, bảng xếp hạng độ đo accuracy trên tập dữ liệu này cho thấy phương pháp tốt nhất hiện tại cũng chỉ đạt ở mức 0.601. Chính vì vậy, với khả năng của các mạng RNN truyền thống, sẽ rất khó để có thể đạt được một kết quả tốt hơn.
