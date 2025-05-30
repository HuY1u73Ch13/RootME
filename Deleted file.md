
# USB Image Forensics Writeup

## Bước 1: Tải về và nhận diện file `.gz`

- Đầu tiên, tôi tải về một tệp `.gz`. Ban đầu, tôi không rõ đây là loại tệp gì.
- Sau khi tìm hiểu, tôi phát hiện `.gz` là định dạng nén sử dụng Gzip — rất phổ biến trên hệ điều hành như Kali Linux.

![{8D3D93CB-7FB0-4421-9CF2-B6DEDB730C26}](https://github.com/user-attachments/assets/db59e155-3115-40ae-b556-c2f319a85998)

## Bước 2: Giải nén `.gz` và kiểm tra định dạng

- Tôi sử dụng lệnh `file` trong terminal để kiểm tra định dạng file vừa giải nén.

![{A38D95A3-8386-440B-9E4B-9833D540B419}](https://github.com/user-attachments/assets/3f7f2508-7c45-4bec-be6e-08544dfab7a3)

- Kết quả cho biết đây là file `.tar`, vậy nên tôi tiếp tục giải nén nó.

![{2C7F27CF-9AD0-44D6-A520-F0F1E5F5477B}](https://github.com/user-attachments/assets/c9bcef55-c0ce-4283-9fa7-e0f108c15d14)

## Bước 3: Phân tích file `usb.image`

- Sau khi giải nén `.tar`, tôi thu được file `usb.image`. Đây là một bản sao (image) của thiết bị USB.
- Có thể xem nó như là một thiết bị USB thật được gắn vào máy.

![{E7937E14-5773-4A0E-AC38-EA94D7B3AEB5}](https://github.com/user-attachments/assets/9067ffa6-670b-4211-b49c-ff4c2d3ecb17)

## Bước 4: Dò tìm dữ liệu ẩn bằng `binwalk`

- Tôi thử mount ảnh USB sang thư mục khác nhưng không thấy gì.
- Phỏng đoán có thể dữ liệu đã bị xoá hoặc ẩn bằng kỹ thuật forensics/steganography.
- Dùng `binwalk` để quét file và trích xuất dữ liệu.

![image](https://github.com/user-attachments/assets/95de2ff0-4e86-428b-98c3-bc870d842ca4)

## Bước 5: Unzip bằng 7-Zip trên Windows

- Không tìm thấy hướng đi rõ ràng từ `binwalk`, tôi thử dùng 7-Zip để giải nén file trên Windows.
- Khi giải nén, tôi thấy một file tên `ch39` không có phần mở rộng. Vì trước đó tôi biết nó là `.tar`, tôi đổi tên file và thêm đuôi `.tar` rồi giải nén.

## Bước 6: Đọc `usb.image` bằng FTK Imager

- Tôi dùng phần mềm FTK Imager để mở file `usb.image`.
- Trong FTK, tôi phát hiện một file ảnh có tên `anonyme.png`.

![{DF3C35EA-5FD1-487F-8107-731048DDDDD2}](https://github.com/user-attachments/assets/b8d6925d-415d-4c63-9624-af546d7b7d0b)

## Bước 7: Phân tích metadata của ảnh

- Mở xem nội dung ảnh dưới dạng plain text, tôi phát hiện dữ liệu dạng XML chứa thông tin `xmp`.

- Kết quả trích xuất được tên: **Javier Turcot**.

---

✅ Kết luận: Dữ liệu ẩn đã được tìm thấy trong metadata của file `.png` thông qua việc phân tích sâu bằng công cụ FTK Imager.
