---
title: Đồng bộ hoá certificates và profiles trong team bằng fastlane match
slug: ''
description: ''
date: 2021-12-13T00:00:00+07:00
author: ThaiLe
tags:
- fastlane
- CICD
cover: "/uploads/fastlane_match.jpg"
fullscreen: false

---
....


## Vì sao chúng ta nên sử dụng *fastlane match*
Fastlane team đã tạo ra trang web để giải thích cặn kẽ cho bạn cách fastlane match làm việc và lý do nó được tạo ra. Bạn có thể **[ đọc thêm ở ĐÂY](https://codesigning.guide/)**.




## Cách cấu hình *fastlane match*
(TODO)

## Cách sử dụng *fastlane match* với certificate có sẵn

> Nếu bạn muốn sử dụng những tính năng hay ho của `fastlane match` trên dự án hiện tại - khi bạn đã có sẵn certificate (.cer) và private key (.p12). Bạn có thể thực hiện được điều đó theo những bước sau đây.

Để import vào encrypt file certificate (.cer), file private key (.p12) và các file provisioning (.mobileprovision) thì bạn sử dụng lệnh:

```bash
fastlane match import
```

Cụ thể hơn, bạn sẽ cần những thứ sau:
+ File certificate (.cer) tải từ trang Apple Development.
+ Private key (.p12) của dự án được cài cho team của bạn.

Giả sử bạn cần import cho môi trường development, hãy chạy lệnh sau:
```
fastlane match import --readonly true --type development
```

Mình sử dụng `--readonly true` để chắc chắn rằng fastlane không tự tạo thêm hoặc thay đổi certificate của chúng ta.
Ngoài ra `--type development` để khai báo sử dụng certificate development. Sử dụng ```type appstore``` cho distribution certificate.

Lệnh trên sẽ yêu cầu bạn nhập vào đường dẫn của những file cần thiết:

```python
Certificate (.cer) path:
# Nhập đường dẫn tới file .cer hoặc bạn có thể kéo thả file đó vào đây

Private key (.p12) path:
# Nhập đường dẫn tới file .p12 hoặc kéo thả file vào đây

Provisioning profile (.mobileprovision or .provisionprofile) path
or leave empty to skip this file:
# Bỏ qua nếu không muốn import những file này
# Ví dụ này chúng ta sẽ bỏ qua việc import provision file
# Chúng ta có thể tự ra provision ở bước sau
```

Như vậy là đã hoàn tất việc import xong certificate. Bạn có thể tạo danh sách provision files hay cách tính năng khác của fastlane match.

```javascript
# Generate provision files of development
fastlane match development
```








