# K58KTP_Web_BT1
## K58KTP - Môn: Phát triển ứng dụng trên nền web
## BÀI TẬP VỀ NHÀ 01:
TẠO SOLUTION GỒM CÁC PROJECT SAU:
DLL đa năng, keyword: c# window library -> Class Library (.NET Framework) bắt buộc sử dụng .NET Framework 2.0: giải bài toán bất kỳ, độc lạ càng tốt, phải có dấu ấn cá nhân trong kết quả, biên dịch ra DLL. DLL độc lập vì nó ko nhập, ko xuất, nó nhận input truyền vào thuộc tính của nó, và trả về dữ liệu thông qua thuộc tính khác, hoặc thông qua giá trị trả về của hàm. Nó độc lập thì sẽ sử dụng được trên app dạng console (giao diện dòng lệnh - đen sì), cũng sử dụng được trên app desktop (dạng cửa sổ), và cũng sử dụng được trên web form (web chạy qua iis).
Console app, bắt buộc sử dụng .NET Framework 2.0, sử dụng được DLL trên: nhập được input, gọi DLL, hiển thị kết quả, phải có dấu án cá nhân. keyword: c# window Console => Console App (.NET Framework), biên dịch ra EXE
Windows Form Application, bắt buộc sử dụng .NET Framework 2.0**, sử dụng được DLL đa năng trên, kéo các control vào để có thể lấy đc input, gọi DLL truyền input để lấy đc kq, hiển thị kq ra window form, phải có dấu án cá nhân; keyword: c# window Desktop => Windows Form Application (.NET Framework), biên dịch ra EXE
Web đơn giản, bắt buộc sử dụng .NET Framework 2.0, sử dụng web server là IIS, dùng file hosts để tự tạo domain, gắn domain này vào iis, file index.html có sử dụng html css js để xây dựng giao diện nhập được các input cho bài toán, dùng mã js để tiền xử lý dữ liệu, js để gửi lên backend. backend là api.aspx, trong code của api.aspx.cs thì lấy được các input mà js gửi lên, rồi sử dụng được DLL đa năng trên. kết quả gửi lại json cho client, js phía client sẽ nhận được json này hậu xử lý để thay đổi giao diện theo dữ liệu nhận dược, phải có dấu án cá nhân. keyword: c# window web => ASP.NET Web Application (.NET Framework) + tham khảo link chatgpt thầy gửi. project web này biên dịch ra DLL, phải kết hợp với IIS mới chạy được.
## Bài làm 
BTVN01 - Love Calculator Solution
Mô tả: Project gồm 4 thành phần: MyLibrary (DLL), ConsoleApp, WinFormsApp, WebApp. Tất cả target .NET Framework 2.0.
Các file quan trọng
1) MyLibrary/LoveCalculator.cs - lớp tính toán chính
2) ConsoleApp/Program.cs - ví dụ dùng DLL trên console
3) WinFormsApp - GUI Windows Forms dùng DLL
4) WebApp - index.html + api.aspx (AJAX) sử dụng DLL

Hướng dẫn build & chạy (tóm tắt)

BTVN01_Solution - Hướng dẫn build & test (target .NET Framework 2.0)

Thư mục chứa:
- MyLibrary/LoveCalculator.cs          (Class Library - tạo MyLibrary.dll)
- ConsoleApp/Program.cs                (Console app - tham chiếu MyLibrary.dll)
- WinFormsApp/Program.cs, Form1.*      (WinForms app - tham chiếu MyLibrary.dll)
- WebApp/index.html, api.aspx, api.aspx.cs (ASP.NET Web Forms) - tham chiếu MyLibrary.dll
- assets/                              (mock screenshots để đính kèm báo cáo)

Hướng dẫn tổng quát (Visual Studio 2005/2008, target .NET 2.0)
1) Tạo Solution mới -> chọn target .NET Framework 2.0.
2) Tạo project Class Library, dán nội dung MyLibrary/LoveCalculator.cs, build -> sinh MyLibrary.dll.
3) Tạo project Console App (.NET 2.0). Trong Solution Explorer -> References -> Add Reference -> Browse -> chọn MyLibrary.dll (từ bin/Debug của project MyLibrary). Dán Program.cs vào, build -> ConsoleApp.exe
4) Tạo project Windows Forms App (.NET 2.0). Thêm tham chiếu tới MyLibrary.dll, dán Program.cs, Form1.cs, Form1.Designer.cs. Build -> WinFormsApp.exe
5) Tạo project ASP.NET Web Application (.NET 2.0). Thêm api.aspx, api.aspx.cs, index.html. Thêm Reference -> Browse -> MyLibrary.dll.
6) Triển khai WebApp trên IIS (local):
   - Copy WebApp thư mục vào một folder ví dụ C:\inetpub\wwwroot\LoveCalcWeb
   - Mở IIS Manager -> Add Website -> Site name: LoveCalcWeb, Physical path: đường dẫn trên, Host name: lovecalc.local (ví dụ)
   - Mở file hosts (C:\Windows\System32\drivers\etc\hosts) dưới quyền admin -> thêm dòng:
        127.0.0.1    lovecalc.local
   - Restart IIS hoặc ứng dụng pool, truy cập http://lovecalc.local/index.html
7) Test AJAX: nhập dữ liệu, nhấn Send -> api.aspx sẽ trả JSON {"percentage": number, "name1":"...","name2":"..."}

Lưu ý:
- Đảm bảo tất cả project target .NET Framework 2.0 (Project Properties -> Target framework).
- Trong .NET 2.0, không có thư viện Json mặc định; ở đây ta trả JSON bằng Response.Write thủ công.
- Nếu gặp lỗi tham chiếu, kiểm tra thư mục bin của web app đã có MyLibrary.dll.
- Nếu sử dụng Visual Studio 2008 Express, vẫn có thể tạo Web Site và Class Library, nhưng phiên bản Express có thể giới hạn 1 số template; dùng Visual Studio full nếu có.
Mockup Screenshots (Kết quả mô phỏng)
console_result.png
 <img width="825" height="206" alt="image" src="https://github.com/user-attachments/assets/f475a000-ba67-4ec1-8df5-914055e75cd9" />

winforms_result.png
 <img width="825" height="550" alt="image" src="https://github.com/user-attachments/assets/8cf272e6-de61-4000-bc4f-411ac4f6a693" />

web_result.png
 `<img width="825" height="458" alt="image" src="https://github.com/user-attachments/assets/8aa5dd76-54eb-4e27-b3ba-584999443d0c" />



 

 

