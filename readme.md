# Temel Git ve Github komutları
**git init** = Git deposu oluşturur

**git add .** = Depoya dosyaları ekler

**git commit -m "commit-name"** = Dosyaları ekleme sebebimizi söyleriz ve commit oluşturulur

**git remote add origin 'url'** = Clouddaki github deposuyla bağlantı kurmamızı sağlar. Url yerine depo urli girilir

**git reset --hard** = En son commite dönmeni sağlar

**git branch** = Aktif olan branchi gösterir

**git branch branch_ismi** = Yeni bir branch oluşturur ve anlık branchdeki kodları kopyalar.

**git push origin --delete branch_ismi** = Clouddaki Branchi siler

**git branch -d branch_ismi** = Local Branchi siler

**git switch branch_ismi** = Localde kullandığın branchi değiştirir


# Klasik bir senaryo

**git init** = Localde repository oluşturulur

**git add .** = Local repository'e dosyalar eklenir

**git commit -m "name"** = Local commit oluşturulur

**git remote add origin url**  = Local repository clouddaki repository'e bağlanır

**git branch main**  = Main branchi oluşturulur ve kodlar main branchine kopyalanır

**git switch main** = Main branchine geçilir

**git push -u origin main** = Local repositorydeki kodları cloud repository'e  atılır.

**git branch -d branch_isim** = Localdeki branch silinir.

**git push origin --delete branch_isim** = İnternetteki branchi silinir.

## Değişiklik ekleneceği zaman ise;
-----
**git branch features/createLoginView** = Branch oluşturulur ve kodlar oraya alınır.

**git switch features/createLoginView** = Branch değiştirilir

**git add .** = Kod yazıldıktan sonra branche eklenir.

**git commit -m "name"** = Yapılan değişiklikler commite girilir.

**git push -u origin features/createLoginView**  = Clouda atılır ve orada branch oluşur.


## Daha sonra githubdan pull request yapılır ve değişiklikler main branchine aktarılır

-------------------------------------

**git switch main** = Main branchine gecersin ve orada eski kodlar olur

**git pull** = Clouddaki main branchini yani güncel halini locale çekersin ve merge edersin

# Spesifik durumlar
- ## Gizli bir repoya bağlanma ve işlem yapma
	Öncelikle SSH key oluşturulması ve github hesabına bu SSH keyin bağlanması gerekiyor.

	**ssh-keygen -t ed25519 -C "your_email@example.com"** = Yeni bir ssh key generate eder

	**eval "$(ssh-agent -s)"** = Anlamını bilmiyorum ama yazmamız gerek

	**ssh-add ~/.ssh/git_key** = SSH key için dosya oluşturulur

	**cat ~/.ssh/git_key.pub** = SSH keyi kopyalar

	Key oluşturmak için localde yapılan işlemler  bu kadar. Daha sonra bu kodu github hesabımıza ekliyoruz.


git pull ile çekerken eğer şu hatayı alırsan
	error: cannot pull with rebase: Your index contains uncommitted changes.
	error: please commit or stash them.
Bu demek oluyor ki yaptığın değişiklikler var ve önce bunları kaydetmen ya da zorla çekip silmen gerekiyor.
Biz burada şunu yapıyoruz. Öncelikle "git stash" ile yaptığımız değişiklikleri arkaplanda kaydediyoruz. Yani yeni bir branch oluşturuyor ve o branche alıyor
Daha sonra git pull ile verilerimizi çekiyoruz. Veriler başarılı bir şekilde geldikten sonra diğer dosyalar silicenektir. 
Fakat biz bunları "git stash" ile kaydettiğimiz için daha sonrasında "git stash pop" yaparak arkaplanda kaydettiğimiz ve silinen verileri tekrardan yüklüyoruz

Belirli bir süre önceki kodları geri almak için yazılan kod:
git reset --hard branch_ismi{"10 minutes ago"}

