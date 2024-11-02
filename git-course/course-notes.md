# Git, Github эхнээс нь дуустал!

## Table of Contents

- [Install Git](#install-git)
- [Delete Git](#delete-git)
- [Setup Remote Git](#setup-remote-git)
- [Git Lifecycle](#git-lifecycle)
- [Unstage Files](#unstage-files)
- [Restore File Change](#restore-file-change)
- [Restore Commits](#restore-commits)
- [Git Branch](#git-branch)
- [Git Merge](#git-merge)

<br>

### Common Git Commands

|     | Git коммандууд                       | Тайлбар                                                                                |
| :-: | :----------------------------------- | :------------------------------------------------------------------------------------- |
|  1  | `brew install git`                   | Homebrew буюу package manager ашиглан Git татаж суулгана                               |
|  2  | `git init`                           | .Git file -ийг төсөл дотроо үүсгэнэ                                                    |
|  3  | `git status`                         | Төслийн өөрчлөлтийг track хийнэ                                                        |
|  4  | `ls -lah`                            | Төсөлтэй холбоотой Git -ийн тохиргоог шалгана                                          |
|  5  | `rm -rf .git`                        | Төсөл дотор үүсгэсэн .Git file болон түүний тохиргоо тэр чигтэй устна                  |
|  6  | `git remote -v`                      | Локал төсөл маань remote repository линктэй холбогдсоныг шалгаж харуулна               |
|  7  | `git remote add origin [HTTPS линк]` | Локал төсөлтэй remote repository линкийг холбоно                                       |
|  8  | `git add -A`                         | Төсөл дээр хийгдсэн бүх шинэчлэлтийг локал git дээр нэмнэ                              |
|  9  | `git commit -m "тайлбар"`            | Локал git дээр нэмсэн бүх өөрчлөлтийг өөрчлөлт болгож баталгаажуулна                   |
| 10  | `git push origin master`             | Локал git дээр баталгаажсан бүх өөрчлөлтийг Github repo -той merge хийнэ               |
| 11  | `git checkout -- .`                  | Локал git дээр хамгийн сүүлд байсан хувилбарын дагуу бүх файлуудыг сэргээнэ            |
| 12  | `rm [filename]`                      | Terminal -аар файл устгана                                                             |
| 13  | `git restore --staged [filename]`    | Stage хийсэн файлыг буцааж болиулна                                                    |
| 14  | `git reset head [filename]`          | Stage хийсэн файлыг буцааж болиулах хоёр дахь арга                                     |
| 15  | `git rm --cached [filename]`         | Stage хийсэн файлыг буцааж болиулах гурав дахь арга                                    |
| 16  | `git restore [filename]`             | Өөрчилсөн файлыг буцааж болиулна                                                       |
| 17  | `git checkout -- [filename]`         | Зөвхөн локал Өөрчилсөн файлыг буцааж болиулна                                          |
| 18  | `git cat-file -p [sha1 hash]`        | Log доторх файлыг дэлгэрүүлж харна                                                     |
| 19  | `git checkout [sha1 hash]`           | Зөвхөн локал Log доторх файлыг дэлгэрүүлж харна                                        |
| 20  | `git checkout master`                | Зөвхөн локал Log доторх файлыг дэлгэрүүлж харна                                        |
| 21  | `git commit -a -m "тайлбар"`         | Modified файлыг нэгэн зэрэг staged болон unmodified төлөвт шилжүүлнэ                   |
| 22  | `cat [filename]`                     | Файл доторх контентыг харна                                                            |
| 23  | `cat .git/head`                      | HEAD файл дотор одоогийн branch (head) аль "sha1hash" хувилбарыг зааж байгааг харуулна |
| 24  | `git branch`                         | Ямар branch -ууд манай repo дотор байгааг харуулна                                     |
| 25  | `git branch [brancname]`             | Repo дотор шинэ branch үүсгэнэ                                                         |
| 26  | `git branch -m [oldName] [newName]`  | Branch -ын нэрийг өөрчилнө                                                             |
| 27  | `git branch -d [branchName]`         | Branch -ыг устгана                                                                     |
| 28  | `git branch -D [branchName]`         | Branch -ыг дотроо файлтай байсан ч устна                                               |
| 29  | `git checkout div`                   | Div branch -руу master branch -аас switch хийнэ                                        |
| 30  | `git merge [branchName]`             | Fast-forward merge: Master branch -аам `git merge [branchName]` гэсэн комманд өгнө     |
| 31  | `git checkout -b [branchName]`       | Зөвхөн локал Repo дотор шинэ branch үүсгээд түүнрүү шилжинэ                            |
| 32  | `git clone [githubRepoHTTPS]`        | Repo дотор шинэ branch үүсгээд түүнрүү шилжинэ                                         |

<br>

#### Install Git

Homebrew буюу package manager ашиглан Git татаж суулгах ба Git файлыг төсөл дотроо үүсгэж, үүсгэсэн эсэхээ шалгаж сурна.

> [!NOTE]
>
> - Эхлээд [Link](https://git-scm.com/downloads/mac) -рүү орно. `$ brew install git` script -ийг уншуулж brew суулгана.
> - Track хийхийг хүссэн төслийн файл дотроо `$ git init` script -ийг уншуулж git файл үүсгэнэ.
> - `$ git status` script -ийг уншуулж одоогийн файлуудын статусыг шалгана.
> - `$ ls -lah` script -ийг уншуулж нуугдсан .git folder үүссэн эсэхийг шалгана.

[Go top](#table-of-contents)

<br>

#### Delete Git

Local ажиллуулж буй төсөл дотор үүссэн .Git файлыг хадгалсан түүх болон тохигооных нь хамт тэр чигт нь устгаж сурна.

> [!NOTE]
>
> - `$ rm -rf .git` script -ийг уншуулснаар төсөл дотор үүсгэсэн .Git file болон түүний тохиргоо тэр чигтэй устна.

[Go top](#table-of-contents)

<br>

#### Setup Remote Git

Local дээр үүсгэсэн файлуудаа Github -тай холбож сурна.

> [!NOTE]
>
> - Github аккаунт үүсгэнэ.
> - Github аккаунт дотроо шинэ repository үүсгэнэ.
> - Үүсгэсэн repository -ийн "<> Code" товчлуур дээр дарахаар HTTPS линк гарч ирэх ба түүнийг хуулж авна.
> - `$ git remote -v` script -ийг уншуулж Github -руу хуулах төсөл нь өөр remote repository -той холбогдоогүй эсэхийг заавал шалгана.
> - `$ git remote add origin [HTTPS линк]` script -ийг уншуулж локал дотор төслөө Github repository -тойгоо холбож өгнө.
> - `$ git remote -v` script -ийг уншуулж холбогдсон эсэхийг шалгана. Холбогдсон тохиолдолд холбосон линк гарч ирэх ётой.
> - `$ git add -A` , `$ git commit -m "Тайлбар"` , `$ git push origin master"` script -ийг уншуулж Github -руугаа локал төслийнхөө файлыг хуулна.

[Go top](#table-of-contents)

<br>

#### Git Lifecycle

Git файлуудын амьдарлын цикл (untracked, modifed, staged, unmodified), устгагдсан төслийг сэргээх, git log түүх харах
Git file -ууд үүсэхээс авхуулаад устах хүртэлх амьдралын цикл буюу статусууд

> [!NOTE]
>
> **Git -ийн статусууд**
>
> - Untracked (Бүртгэлгүй)
>   - Unmodified төлвийн файлыг буцааж бүртгэлгүй болговол энэ төлөвт шилждэг
> - Modified (Өөрчлөгдсөн)
>   - Unmodified төлөвтэй байсан файлыг өөрчилж, устгавал энэ төлөвт шилждэг
> - Staged (Сонгогдсон)
>   - Untracked эсвэл Modified төлвөөс `git add` комманд өгч уг төлөврүү шилжинэ
> - Unmodified (Өөрчлөлтгүй)
>   - Staged төлвөөс `git commit` комманд өгч уг төлөвт шилжинэ

> [!NOTE]
>
> - `$ git checkout -- .` script -ийг уншуулж хамгийн сүүлд байсан хувилбарын дагуу бүх файлуудыг сэргээнэ.

[Go top](#table-of-contents)

<br>

#### Unstage Files

Stage хийсэн файлуудыг болиулах 3 арга байдаг

> [!NOTE]
>
> - git restore --staged [filename]
> - git reset head [filename]
> - git rm --cached [filename]

[Go top](#table-of-contents)

<br>

#### Restore File Change

Өөрчилсөн folder эсвэл file -ыг буцааж болиулах 2 арга байдаг

> [!NOTE]
>
> - git restore [filename]
> - git checkout -- [filename]

[Go top](#table-of-contents)

<br>

#### Restore Commits

`git log` ашиглан төслийн бүх commit -уудыг харна. Тухайн commit -уудаас хүссэн цаг үеийг `git checkout [sha1 hash]` script ашиглан дахин сэргээж, тэр үеийн файлын хувилбараас branch үүсгэн ажиллах боломжтой. Эсвэл `git checkout master` script ашиглан хамгийн сүүлийн хувилбар -руу буцаж очих боломжтой.

> [!NOTE]
>
> - git checkout [sha1 hash]
> - git checkout master

[Go top](#table-of-contents)

<br>

#### Git Branch

Developer -ын ажиллаж буй Branch -ыг .git файл дотроос харна. `git branch div` гэсэн script -ээр шинэ div branch үүсгэнэ. Branch -ийн нэрийг `git branch -m [oldBranchName] [newBranchName]` гэж өөрчилнө. `git branch d [BranchName]` гэсэн command -аар branch -ийг устгана.

> [!NOTE]
>
> - cat .git/HEAD
> - cat [filename]
> - cd .git/refs/heads/master
> - git branch
> - git branch [branchName]
> - git branch -m [oldName] [newName]
> - git branch d [branchName]

[Go top](#table-of-contents)

<br>

#### Git Merge

Master branch дээр ямар ч өөрчлөлт хийлгүйгээр шинэ branch үүсгэж өөрчлөлт хийж явж байгаад merge хийх үед Fast-forward хэлбэрээр хийгддэг. Master branch -аас `git merge [branchName]` гэсэн комманд өгнө.

> [!NOTE]
>
> - git merge [branchName]

[Go top](#table-of-contents)

<br>
