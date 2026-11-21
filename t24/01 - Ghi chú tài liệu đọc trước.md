---
title: T24 — Ghi chú tài liệu đọc trước
tags:
  - t24
  - source-notes
---

# Ghi chú tài liệu đọc trước

Đã đọc nội dung trong `OneDrive_1_11-21-2026/0. Tài liệu đọc trước`. Thư mục gồm 4 PDF, 1 DOCX và 1 ZIP. ZIP chứa lại `11.Subroutine Guide.pdf`, `5.Temenos T24 - Common Variables.pdf`, `8.Temenos T24 - Right Ho, T24.pdf` và `Hướng dẫn auto compile VSCODE.docx`; đó là bản sao, không phải 4 tài liệu mới.

## 1. T24 Development & Integration Mastery — tổng quan khóa học (PDF)

- Mô tả core banking như sổ trung tâm để ngân hàng vận hành tiền có kiểm soát.
- Nhấn mạnh hai khối nghiệp vụ cốt lõi: **General Ledger (GL)** là sổ cái/kế toán trung tâm; **Arrangement Architecture (AA)** là bộ máy cấu hình và quản lý sản phẩm.
- Đặt T24/Transact vào bối cảnh hệ sinh thái: tích hợp OFS/ESB, kênh số như Infinity, nền tảng TAFJ và xử lý cuối ngày **COB**.
- Thông điệp học tập: nền tảng tham số hóa cho phép tạo nhiều sản phẩm; COB đáp ứng nhu cầu nghiệp vụ và pháp lý, không chỉ là thao tác kỹ thuật.
- Giới hạn nguồn: tài liệu là slide nhập môn, nên một số chủ đề chỉ có tiêu đề/ý chính. Dùng để tạo khung nghiệp vụ, không làm căn cứ cấu hình production.

## 2. Right Ho, T24 — kỹ thuật T24/jBASE (PDF, V. Kazimirchik, cập nhật 2015)

Đây là cẩm nang kỹ thuật dài, trình bày bằng ví dụ theo kiểu tutorial. Mạch nội dung trong mục lục:

| Chủ đề | Vị trí trong PDF | Ghi nhớ |
|---|---:|---|
| T24, jBASE, TAFC/TAFJ, jsh, jBC, jQL; môi trường và đăng nhập | tr. 6–26 | Phân biệt runtime, shell, ngôn ngữ và kho dữ liệu; nhiều ví dụ nhắm TAFC/jBASE cũ. |
| Ứng dụng, thao tác record, hàm T24, chương trình jBC đầu tiên | tr. 26–61 | Tập đọc môi trường và record trước khi viết xử lý. |
| Multi-value, subroutine, ngày giờ, đọc record kiểu T24, concat file, pattern | tr. 49–69 | Hiểu cấu trúc dữ liệu multi-value và dùng abstraction T24 phù hợp. |
| Lock, VERSION, vòng đời application, validation và hook | tr. 69–100 | Học luồng nhập–validate–authorize và các điểm mở rộng. |
| OFS, bảng ký tự, IN2, report/file, log OFS, override | tr. 100–129 | Xem thông điệp tích hợp, log, lỗi và cách xử lý override. |
| R.NEW/R.OLD/R.NEW.LAST, history, ENQUIRY và OFS nâng cao | tr. 129–177 | Làm rõ trạng thái record, lịch sử và truy vấn nghiệp vụ. |
| Local fields, routines, I/J-descriptor, jQL, category và loại application | tr. 177–213 | Nối metadata với hiển thị/truy vấn và mở rộng cục bộ. |
| Giao dịch, F.PROTOCOL, bút toán, tSM/tSA, COB và lock | tr. 213–247 | Nối một giao dịch với dấu vết protocol, kế toán và xử lý ngày. |
| Enquiry routine, JBoss/browser settings, local app, delivery, NOFILE enquiry | tr. 247–289 | Tham khảo khi triển khai/tích hợp trong lab đúng cấu hình. |
| Cookbook jBC, compile/catalog, jQL, file và chẩn đoán | khoảng tr. 290–367 | Tra cứu theo vấn đề cụ thể; kiểm tra lệnh với release đang dùng. |

**Điểm chính:** T24 chạy logic ứng dụng chủ yếu bằng jBC/Infobasic trong hướng dẫn này; dữ liệu kiểu multi-value, application/version, các hàm đọc/ghi và trạng thái hồ sơ tạo thành nền tảng để hiểu luồng giao dịch. Tác giả mô tả jBASE là post-relational và phân biệt TAFC (C) với TAFJ (Java). Mô tả này gắn với thời điểm tài liệu; đừng suy diễn rằng mọi hệ thống hiện tại có cùng kiến trúc.

## 3. Subroutine Guide — tra cứu routine (PDF)

Hướng dẫn khuyến nghị ưu tiên routine chuẩn khi T24 đã cung cấp routine cho một tác vụ; Temenos có thể thay đổi routine theo thời gian. Các nhóm nổi bật:

- **Ngày/thời gian:** CDD (chênh lệch ngày), CDT (dịch ngày làm việc/lịch), CFQ và các routine chuyển đổi lịch/ngày.
- **Tỷ giá/tiền tệ:** CALC.ERATE.LOCAL, CUSTRATE, EXCHRATE, DIFFERENCE, BASE.CCY, FCY.CONVERT.CHECK.
- **Truy cập file/record:** OPF, F.READ/F.READU, F.WRITE, F.DELETE, F.MATREAD/F.MATWRITE, F.LIVE.WRITE; các routine lock và transaction abort.
- **Validation và thông báo:** DUP, FT.NULLS.CHK, STORE.END.ERROR, STORE.OVERRIDE, REBUILD.SCREEN; các routine text/message như APP.STATIC.TEXT, ERR, OVE, REM.
- **Nghiệp vụ và tiện ích:** batch update, phí, số tiền nội tệ/làm tròn, narrative, giới hạn, settlement defaults, selection details, printing/spool.

**Cách dùng:** tra đúng chữ ký tham số, kiểu dữ liệu và yêu cầu INSERT trong release cụ thể. Danh sách PDF là tài liệu tham khảo, không thay thế API/standard routines guide hiện hành.

## 4. Common Variables — các biến dùng chung (PDF, bài viết 2014)

Các biến được mô tả là khả dụng khi chèn `I_COMMON`. Nhóm đáng nhớ:

- **Record:** `R.COMPANY`, `R.DATES`, `R.NEW`, `R.NEW.LAST`, `R.OLD`, `R.USER`, `R.VERSION`.
- **Vị trí field multi-value/sub-value:** `A`, `AF`, `AV`, `AS`, `VM`; hiểu khác biệt giữa chỉ số hiển thị và field vật lý trước khi sửa dữ liệu.
- **Luồng input/validation:** `COMI`, `COMI.DEFAULT`, `COMI.ENRI`, `DISPLAY`, `ANY.INPUT`, `END.ERROR`, `ETEXT`, `ECOMI`.
- **Ngữ cảnh ứng dụng/người dùng:** `APPLICATION`, `FUNCTION`, `AUTH.NO`, `AUTH.QUALITY`, `OPERATOR`, `ID.COMPANY`, `PGM.TYPE`, `PGM.VERSION`.
- **Màn hình/thời gian:** `SCREEN.MODE`, `L1ST`, `LASTP`, `TODAY`, `TODAY.VERSION`, `TIME.STAMP`, `TNO`.

Tài liệu có nhiều định nghĩa lịch sử và ví dụ chi tiết; tra cứu theo tên biến thay vì học thuộc toàn bộ. Xác minh với include và compiler của hệ thống thực tế vì bộ biến có thể đổi theo release/module.

## 5. Hướng dẫn auto compile VS Code (DOCX)

- Cài extension `Run on Save` và extension syntax cho Rocket MV BASIC.
- Gán file `.vn` và `.b` sang ngôn ngữ Rocket MV BASIC; cấu hình formatter.
- Ví dụ `emeraldwalk.runonsave` chạy `tCompile.bat` khi lưu file `.b`, truyền `${file}`; dùng JDK và thư mục TAFJ dưới `D:\DEV\Temenos\R25\...`.
- Đường dẫn R25/JDK, biến môi trường và câu lệnh compile trong tài liệu là ví dụ theo một máy/lab cụ thể. Thay bằng đường dẫn do quản trị viên cấp; không chép nguyên cấu hình vào máy hoặc server khác.

## Từ điển kết nối

| Từ khóa | Ý nghĩa học tập |
|---|---|
| T24 / Transact | Nền tảng core banking Temenos; Transact là tên thương mại mới được slide nêu. |
| AA | Cấu hình/vận hành vòng đời sản phẩm theo nội dung nhập môn. |
| GL | Sổ cái kế toán ghi nhận ảnh hưởng tài chính. |
| OFS | Cơ chế thông điệp tích hợp với T24 trong các tài liệu. |
| jBC / jBASE / jQL | Ngôn ngữ ứng dụng, nền tảng dữ liệu và ngôn ngữ truy vấn trong cẩm nang kỹ thuật. |
| VERSION | Cấu hình màn hình/luồng ứng dụng và kiểm tra đầu vào trong tutorial. |
| COB | Chu trình xử lý cuối ngày, có liên hệ tới tính lãi, kế toán và ngày nghiệp vụ. |

## Nguồn đã đọc

1. `3.2.0. Thông tin chương trình T24 Development & Integration Mastery.pdf`
2. `8.Temenos T24 - Right Ho, T24.pdf` — V. Kazimirchik, bản cập nhật ghi trong PDF: 05-04-2015.
3. `11.Subroutine Guide.pdf`
4. `5.Temenos T24 - Common Variables.pdf` — nội dung ghi nguồn wikibanking.info, 23-05-2014.
5. `Hướng dẫn auto compile VSCODE.docx`
6. `T24 tài liệu DEV 2111.zip` — archive chứa lại 3 PDF kỹ thuật và DOCX nêu trên.

> Độ mới: Subroutine Guide và hai tài liệu kỹ thuật không xác nhận release hiện hành. Dùng chúng để học khái niệm; xác thực mọi cú pháp, biến, routine, cấu hình compile và vận hành theo môi trường/lab được cấp.
