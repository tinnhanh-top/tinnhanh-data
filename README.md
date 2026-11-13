# Dữ liệu tài chính Việt Nam theo ngày

Lãi suất tiết kiệm, giá vàng, tỷ giá ngoại tệ, giá xăng dầu và điểm chỉ số chứng khoán Việt Nam, mỗi ngày một dòng cho mỗi mã. [TinNhanh](https://tinnhanh.top/du-lieu) lấy số từ bảng giá công khai của các ngân hàng, PNJ, Vietcombank, Saigon Petro và DNSE, rồi đưa lên kho này mỗi tối.

Cập nhật lần cuối: 13/11/2026 10:40 (giờ Việt Nam).

## Các file

| File | Nội dung | Từ ngày | Đến ngày | Số dòng |
|---|---|---|---|---:|
| [data/lai-suat.csv](data/lai-suat.csv) | Lãi suất tiết kiệm theo ngày của 8 ngân hàng | 09/11/2026 | 13/11/2026 | 431 |
| [data/gia-vang.csv](data/gia-vang.csv) | Giá vàng miếng SJC và vàng nhẫn theo ngày | 02/11/2026 | 13/11/2026 | 24 |
| [data/ty-gia.csv](data/ty-gia.csv) | Tỷ giá ngoại tệ Vietcombank theo ngày | 02/11/2026 | 13/11/2026 | 96 |
| [data/gia-xang.csv](data/gia-xang.csv) | Giá xăng dầu bán lẻ theo ngày | 09/11/2026 | 13/11/2026 | 20 |
| [data/chi-so.csv](data/chi-so.csv) | Điểm đóng cửa VN-Index, VN30, HNX-Index, UPCoM-Index | 10/08/2026 | 13/11/2026 | 268 |

## Định dạng

- CSV mã UTF-8 (có BOM), dấu phẩy ngăn cột, dấu chấm thập phân. Ngày dạng `YYYY-MM-DD` theo giờ Việt Nam.
- Mỗi dòng là mức của một mã trong một ngày, lấy theo lần cập nhật cuối của ngày đó. Ngày không có dòng là ngày không lấy được số; giá xăng và chỉ số chứng khoán chỉ có ngày có kỳ giá hoặc phiên giao dịch.
- Ô trống là nguồn không công bố mức đó (ví dụ Vietcombank không mua tiền mặt một số ngoại tệ).
- Excel cài tiếng Việt có thể đọc sai số thập phân. Khi đó tải bản Excel ở [tinnhanh.top/du-lieu](https://tinnhanh.top/du-lieu), hoặc mở bằng Google Sheets, Python, R.

```python
import pandas as pd
gia_vang = pd.read_csv("https://raw.githubusercontent.com/tinnhanh-top/tinnhanh-data/main/data/gia-vang.csv", parse_dates=["ngay"])
```

## Lãi suất tiết kiệm theo ngày của 8 ngân hàng

Lãi suất tiết kiệm VND của khách hàng cá nhân, lĩnh lãi cuối kỳ, tại quầy và online, theo từng kỳ hạn, mỗi ngày một mức: Vietcombank, BIDV, VietinBank, Agribank, Techcombank, ACB, Sacombank, TPBank.

Nguồn: Biểu lãi suất công bố trên website của từng ngân hàng. Kiểm tra khoảng 6 giờ một lần, mỗi ngày lưu mức của lần kiểm tra cuối. Số hôm nay: [tinnhanh.top/lai-suat](https://tinnhanh.top/lai-suat).

| Cột | Ý nghĩa |
|---|---|
| `ngay` | Ngày (YYYY-MM-DD, giờ Việt Nam) |
| `ma_ngan_hang` | Mã ngân hàng (VCB, BIDV, CTG…) |
| `ngan_hang` | Tên ngân hàng |
| `hinh_thuc` | tai_quay hoặc online |
| `ky_han_thang` | Kỳ hạn (tháng) |
| `lai_suat` | Lãi suất (%/năm) |

## Giá vàng miếng SJC và vàng nhẫn theo ngày

Giá mua vào và bán ra của vàng miếng SJC và nhẫn trơn PNJ 999.9 theo bảng giá PNJ, mỗi ngày một mức, đơn vị triệu đồng/lượng.

Nguồn: Bảng giá vàng của PNJ. Kiểm tra khoảng 30 phút một lần, mỗi ngày lưu giá của lần cập nhật cuối. Số hôm nay: [tinnhanh.top/gia-vang](https://tinnhanh.top/gia-vang).

| Cột | Ý nghĩa |
|---|---|
| `ngay` | Ngày (YYYY-MM-DD, giờ Việt Nam) |
| `ma` | Mã loại vàng (SJC, N24K) |
| `loai_vang` | Tên loại vàng |
| `mua_vao` | Giá mua vào (triệu đồng/lượng) |
| `ban_ra` | Giá bán ra (triệu đồng/lượng) |

## Tỷ giá ngoại tệ Vietcombank theo ngày

Tỷ giá mua tiền mặt, mua chuyển khoản và bán ra của 8 ngoại tệ (USD, EUR, JPY, GBP, CNY, KRW, AUD, SGD) tại Vietcombank, mỗi ngày một mức, đơn vị đồng.

Nguồn: Bảng tỷ giá của Vietcombank. Kiểm tra khoảng 30 phút một lần, mỗi ngày lưu tỷ giá của lần cập nhật cuối. Số hôm nay: [tinnhanh.top/ty-gia](https://tinnhanh.top/ty-gia).

| Cột | Ý nghĩa |
|---|---|
| `ngay` | Ngày (YYYY-MM-DD, giờ Việt Nam) |
| `ma` | Mã ngoại tệ |
| `ngoai_te` | Tên ngoại tệ |
| `mua_tien_mat` | Giá mua tiền mặt (đồng) |
| `mua_chuyen_khoan` | Giá mua chuyển khoản (đồng) |
| `ban_ra` | Giá bán ra (đồng) |

## Giá xăng dầu bán lẻ theo ngày

Giá bán lẻ xăng E10 RON 95, E5 RON 92 và dầu diesel tại vùng 1, mỗi ngày một mức, đơn vị đồng/lít.

Nguồn: Bảng giá bán lẻ của Saigon Petro. Kiểm tra khoảng 30 phút một lần; giá chỉ đổi ở các kỳ điều hành. Số hôm nay: [tinnhanh.top/gia-xang](https://tinnhanh.top/gia-xang).

| Cột | Ý nghĩa |
|---|---|
| `ngay` | Ngày (YYYY-MM-DD, giờ Việt Nam) |
| `ma` | Mã mặt hàng |
| `mat_hang` | Tên mặt hàng |
| `gia_ban_le` | Giá bán lẻ (đồng/lít) |

## Điểm đóng cửa VN-Index, VN30, HNX-Index, UPCoM-Index

Điểm đóng cửa theo phiên của các chỉ số chứng khoán VN-Index, VN30, HNX-Index và UPCoM-Index. Phiên đang giao dịch là điểm mới nhất lúc cập nhật.

Nguồn: Dữ liệu chỉ số từ DNSE (chỉ số do HOSE, HNX công bố). Cập nhật sau mỗi phiên giao dịch. Số hôm nay: [tinnhanh.top/vn-index](https://tinnhanh.top/vn-index).

| Cột | Ý nghĩa |
|---|---|
| `ngay` | Ngày giao dịch (YYYY-MM-DD) |
| `ma` | Mã chỉ số |
| `chi_so` | Tên chỉ số |
| `diem_dong_cua` | Điểm đóng cửa |

## Nguồn và quyền sử dụng

Số liệu gốc thuộc các ngân hàng, PNJ, Vietcombank, Saigon Petro và các sở giao dịch chứng khoán. TinNhanh chỉ tổng hợp và lưu theo ngày, không cấp giấy phép thay các bên này, nên kho không kèm file LICENSE.

Khi dùng trong bài viết hay nghiên cứu, vui lòng ghi nguồn, ví dụ: “Nguồn: TinNhanh tổng hợp từ bảng giá PNJ, tinnhanh.top/du-lieu”.

Số liệu chỉ để tham khảo, có thể thiếu ngày hoặc lệch so với nguồn, không phải khuyến nghị đầu tư.

Thấy số sai hoặc cần dữ liệu cũ hơn: mở issue ở kho này hoặc [liên hệ TinNhanh](https://tinnhanh.top/lien-he).
