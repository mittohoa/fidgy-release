# Fidgy — kênh phát hành

**Tải app tại đây: https://mittohoa.github.io/fidgy-release/**

Repo này chỉ chứa bản kê phiên bản, trang tải và các file cài đặt của **Fidgy**.
Mã nguồn nằm ở repo riêng.

| File | Vai trò |
| --- | --- |
| `index.html` | Trang tải, chạy trên GitHub Pages |
| `version.json` | App đọc file này để biết có bản mới hay không |
| Mục **Releases** | File APK của từng bản |

## Cài đặt

Vào [trang tải](https://mittohoa.github.io/fidgy-release/) rồi bấm **Tải cho
Android**. Mở file `.apk` vừa tải, Android sẽ hỏi cho phép cài ứng dụng từ nguồn
này — chọn Cho phép. Máy chỉ hỏi một lần.

Từ lần sau app tự báo khi có bản mới, tải ở nền rồi cài đè — nhật ký và tiến độ
chơi được giữ nguyên.

## Phát hành một bản mới

Chạy trong repo mã nguồn:

```bash
# 1. Sửa version trong pubspec.yaml, ví dụ 1.0.2+3
flutter build apk --release
dart run tool/make_release.dart "Ghi chú của bản này"
```

Rồi mang sang repo này:

```bash
cp <mã-nguồn>/build/app/outputs/flutter-apk/app-release.apk Fidgy-1.0.2.apk
cp <mã-nguồn>/version.json .
gh release create v1.0.2 Fidgy-1.0.2.apk --repo mittohoa/fidgy-release \
   --title "Fidgy 1.0.2" --notes-file notes.txt
git add version.json && git commit -m "Bản 1.0.2" && git push
```

Trang tải tự đọc `version.json` nên không phải sửa `index.html`.

> **Mọi bản APK phải ký cùng một keystore.** Khác khoá là Android từ chối cài đè
> và người chơi mất hết nhật ký. Khoá nằm ngoài repo — nhớ giữ bản sao.
