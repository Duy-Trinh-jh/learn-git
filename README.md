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

## Basic git command

- Git add: dùng để thêm một hoặc nhiều file thay đổi đến stage/index ở bên trong thư mục làm việc.
```
git add <filename> or git add .
```
- Git push / git pull: Push hoặc Pull là các thay đổi đến remote. Nếu bạn đã add và committed các thay đổi rồi bạn muốn đẩy nó lên hoặc remote của bạn đã update thì bạn sẽ apply tất cả thay đổi đó trên code của mình.
```
git pull <:remote:> <:branch:> and git push <:remote:> <:branch:>
```
- Git stack: dùng để lưu các thay đổi mà bạn không muốn commit ngay lập tức. 
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
- Git merge: dùng merge branch khác vào branch hiện tại mình đang làm:
```
git merge <branchname>
```
- Git rebase: dùng để nhập một branch đã gần hoàn thiện vào branch gốc (branch master) một cách tuyến tính
```
git rebase  <branchname>  
```

## Conflict

### Nguyên nhân gây ra conflicts
- Công việc của bạn với người khác cùng thay đổi các file giống nhau, việc bạn chỉnh sửa file sẽ ảnh hưởng trực tiếp tới người đó. Do đó cần thảo luận với đồng nghiệp về phạm vi công việc cho nó rõ ràng để loại bỏ sự chồng chéo.
- Do cách tổ chức nhánh hoặc quy trình làm việc. Do đó khi làm việc thì cần tạo mới một branch cho bản thân và xác định rõ công việc của mình
- Xung đột với chính mình do repo trên máy chưa được cập nhật theo cái mới nhất, có thể do có người nào đó làm việc chung thay đổi trên branch làm cho repo trên máy bị lỗi thời. Hoặc có thể bạn đang làm việc trên quá nhiều nhánh mà chưa hợp nhất sự thay đổi trên các nhánh lại thành một nhánh.

### Cách giải quyết conflict và hạn chế conflict
- Chỉnh sửa nội dung trên file mà nó dẫn tới xung đột, sau đó thực hiện add, commit cho file đó.
- Nên commit thường xuyên: không nên commit một lượng lớn file mà hãy chia nhỏ để commit để có thể dễ dàng giải quyết conflict
- Trước khi làm việc hoặc commit cần pull những thay đổi từ github về
- Nên tách từng feature thành từng branch riêng biệt để người làm hạn chế gây conflict với nhau.

## Merge và Rebase

### So sánh Merge và Rebase
Giống: Đều dùng để hợp nhất code tại 2 nhánh lại với nhau
Khác nhau: 
- git merge khi gộp vào vẫn giữ nguyên sự sắp xếp các commit theo thứ tự thời gian của các commit trên các nhánh. lệnh merge sẽ so sánh nội dung 3 commit: commit ở điểm rẽ nhánh giữa 2 nhánh cần merge và 2 commit cuối của 2 nhánh cần gộp. Sau đó nó sẽ gộp lại thành một commit tổng hợp đã được xử lý xung đột (nếu có). Git merge làm những nhánh đang tồn tại không bị thay đổi.
- git rebase sẽ đưa toàn bộ commit của nhánh cần merge làm base và nếu có xung đột xảy ra thì sẽ tiến hành sửa đổi lịch sử commit tại commit gây ra xung đột, sau đó nối tiếp các commit kế tiếp của nhánh hiện tại. Git rebase làm cho lịch sử commit có dạng tuyến tính xuyên suốt từ đầu đến hiện tại.

### Kết hợp Merge và Rebase
Cả hai đều dùng để hợp nhất code tại 2 nhánh lại với nhau. Do đó tùy vào mục đích ta sử dụng git rebase nếu như muốn các sự thay đổi thuộc về branch của mình luôn luôn là mới nhất và có thể log một cách có hệ thống dễ nhìn, dễ tracking sau này. Hoặc ta sử dụng git merge nếu muốn sắp xếp các commit theo mặc định.

Để giữ lại các commit ở nhánh phụ trên nhánh master khi tiến hành hợp nhất 2 nhánh, chúng ta có thể rebase nhánh master ở nhánh phụ trước rồi sau đó merge nhánh phụ vào nhánh master. Điều này giúp tránh mất đi các commit trên nhánh phụ ở nhánh master.

## Exercise
### Description: We have 2 big branch call master (to hold test features for test site) & production. 
### Exercise 1: (Ap & Ev) When we are creating new feature, what branch should we based on and why?
- Khi chúng ta xây dựng một feature mới, ta nên dựa trên nhánh master bởi vì nhánh master sẽ chứa test features để ta có thể test kỹ feature trước khi merge qua nhánh master và sau đó tính năng ấy sẽ an toàn để merge vào nhánh production để deploy.
```
git checkout master
git branch <new-feature>
git checkout <new-feature>
```
### Exercise 2: (Ap) If we have a feature branch that haven't been merged to production and that branch have bug, what course of action are you going to do with Git to before resolving the bug?
- Ta checkout nhánh của feature đó rồi sau đó ta sẽ tạo một branch mới để fix bug từ nhánh hiện tại.

### Exercise 3: (Ap & Ev) If someone accidentally merge a feature (feature/delete-user) onto production and have a list of commitId ended with (0492978, fc9348c, k101100), then another commit (a1fsas8) is added on top of the production branch. How do we remove that merged feature?
- Ta sẽ sử dụng git revert để xử lý
```
git checkout production
git revert -m 1 a1fsas8
git revert -m 1 k101100
git revert -m 1 fc9348c
git revert -m 1 0492978
```