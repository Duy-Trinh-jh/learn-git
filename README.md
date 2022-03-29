# learn-git
## Git là gì và lợi ích của nó

### Khái niệm
> Git là một hệ thống quản lý phiên bản phân tán. Nó giúp cho lập trình viên có thể sử dụng để lưu trữ code, quản lý lịch sử thay đổi cũng như chia sẻ cho người khác.

### Lợi ích của Git
- Có thể tách công việc thành từng phần riêng để mọi người làm việc đồng thời với nhau
- Dễ dàng thử nghiệm những phần mới mà không lo bị ảnh hưởng tới phiên bản chính thức
- Quản lý được lịch sử thay đổi từ đó có thể kiểm tra lại trong trường hợp có sự cố xảy ra
- Linh hoạt cho làm việc, mọi người có thể làm việc tại bất cứ nơi đâu miễn là có quyền truy cập vào repo
- Git đảm bảo không có xung đột mã nguồn giữa các lập trình viên trong một dự án
- Git miễn phí

## Commit 

### Commit là gì?
> Commit được sử dụng để lưu lại phần thay đổi tới local Repo. Nó thường đi kèm với message để mô tả ngắn gọn phần thay đổi.

Commit options:
- -m: Để ghi ra mô tả cho commit
```
git add index.html
git commit -m "message"
```
- -a hoặc -all: Để commit hết tất cả các file (tạo mới, có chỉnh sửa hoặc bị xóa)
```
git commit -a -m "message"
```

- -amend: viết lại message cho commit
```
git commit -amend
```
### Cách viết message tốt:

Cú pháp:
```
git commit -m "Subject" -m "Description..."
```

Cách viết commit tốt:
- Phân loại loại commit:
  - feat: thêm feature mới vào project
  - fix: sửa lỗi
  - style: các cập nhật liên quan tới styling
  - refactor: tất cả thay đổi về file có sẵn
  - test: tất cả các phần liên quan tới testing project
  - docs: tất cả các phần liên quan tới viết tài liệu
- Luôn bắt đầu message bằng một động từ
- Không chấm cuối câu
- Viết hoa chữ cái đầu message hoặc đoạn văn
- Không được cho rằng việc giải thích commit bằng code
- Tuân theo cách commit đã được thống nhất trong team

### Các lỗi có thể xảy ra với commit:
- Viết sai message trong commit, cách sửa lỗi ta phải sử dụng -amend:
```
git commit -amend
```
- commit sai mà người khác đã pull về và ta muốn xóa commit đó:
```
# commit_hash là mã commit
git revert <commit_hash>
```
- Lỡ commit nhầm sang một branch khác
```
#Đầu tiên là tạo một branch khác chứa trạng thái mà ta đã commit
$ git branch other-branch
#Đưa HEAD, index của master về 1 commit trước đó
$ git reset --hard HEAD~
#Check out sang branch có commit trước đó
$ git checkout other-branch
```
- Lỡ tay xóa nhầm commit quan trọng, cách xử lý:
```
# Đầu tiên là xem lại toàn bộ lịch sử commit
$ git reflog
# Từ đó chọn commit muốn phục hồi và khôi phục lại
# ví dụ: git reset --hard HEAD@{2}
$ git reset --hard <commit>
```

## Branch

### Git command for branch
Lệnh sẽ thực hiện liệt kê tất cả các branch (nhánh):
```
git branch hoặc git branch -a
```
Lệnh này có tác dụng chuyển sang một branch khác:
```
git checkout feature
```
Lệnh này sẽ tạo hoặc chuyển sang một nhánh mới:
```
git checkout -b new_feature
```

### Các lỗi có thể xảy ra với Branch:
- Đặt sai tên branch, ta có thể rename lại tên branch:
```
git branch -m <tên branch sau khi đổi>
```
- Chuyển sang nhánh khác nhưng chưa sao lưu lại công việc đang làm dở có thể làm mất code, ta có thể xử lý như sau:
```
# Tạm thời lưu lại các phần công việc còn đang làm dở
$ git stash -u
# Chuyển sang một branch khác và làm việc
$ git checkout -b other-branch
$ git add <các file cần thiết>
$ git commit -m "commit message"
# Trở về branch cũ
$ git checkout origin-branch
# Lấy lại các nội dung công việc đang làm dở trước đó
$ git stash pop
```
- Lỡ tay xóa nhầm đi branch, ta có thể giải quyết như sau:
```
# Đầu tiên là xem lại toàn bộ lịch sử commit
$ git reflog
# Từ các commit này, chọn rồi tạo branch mới
# ví dụ: git branch new-branch HEAD@{2}
$ git branch <tên branch> <commit_id>
```