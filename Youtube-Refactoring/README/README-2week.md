### ๐ 2์ฃผ์ฐจ ๊ณผ์  ๋ฆฌ๋๋ฏธ
<br/>

- [x] ๋ก๊ทธ์ธ ํ๋ฉด AutoLayout ์ ์ฉํ๊ธฐ
- [x] ํ์๊ฐ์ ํ๋ฉด AutoLayout ์ ์ฉํ๊ธฐ
- [x] ํ์ธ ํ๋ฉด AutoLayout ์ ์ฉํ๊ธฐ
- [x] ํ์ธ ํ๋ฉด์ "๋ค๋ฅธ ๊ณ์ ์ผ๋ก ๋ก๊ทธ์ธํ๊ธฐ" ๋ฒํผ ์ถ๊ฐํ๊ธฐ
- [x] ํ์ธ ํ๋ฉด์ "๋ค๋ฅธ ๊ณ์ ์ผ๋ก ๋ก๊ทธ์ธํ๊ธฐ ๋ฒํผ ์ถ๊ฐ" ๋๋ฅด๋ฉด ์ฒ์ ๋ก๊ทธ์ธ ํ๋ฉด์ผ๋ก ๋์๊ฐ๊ธฐ
- [x] ํ์ธ ํ๋ฉด์์ ํ์ธ ํ๋ฉด ๋๋ฅด๋ฉด Tabbar๋ก ์ฐ๊ฒฐ๋ ํ๋ฉด Present ํ๊ธฐ
- [x] Tabbar์ 5๊ฐ์ view controller ์ฐ๊ฒฐํ๊ธฐ
- [x] tabbar title, image, selected image ๋ฐ๊พธ๊ธฐ

---
#### โจ AutoLayout ์ ์ฉํ๊ธฐ & ๋ค๋ฅธ ๊ณ์ ์ผ๋ก ๋ก๊ทธ์ธ ํ๊ธฐ ๋ฒํผ ์ถ๊ฐ 

![image](https://user-images.githubusercontent.com/81313960/137844974-c74d556e-9dd3-4e8b-8612-ee8fe5c8234e.png)

#### ๐ฎ TabbarController 

1. Tabbar ํ๋ฉด ๊ตฌ์ฑํ๊ธฐ 

![Simulator Screen Recording - iPhone 13 - 2021-10-19 at 13 51 54](https://user-images.githubusercontent.com/81313960/137846074-c6d69f15-9ce3-4ba7-8f51-e8cf77f34821.gif)

2. ํ์ธ ๋ฒํผ ๋๋ฅผ ์, ํญ๋ฐ ํ๋ฉด์ผ๋ก ์ด๋
```swift
@IBAction func confirmButton(_ sender: Any) {
        let tabBarStoryboard = UIStoryboard.init(name: "TabBar", bundle: nil)
        
        guard let tabbar = tabBarStoryboard.instantiateViewController(withIdentifier: "TabBarController") as? TabBarController else {return}
        
        tabbar.modalPresentationStyle = .fullScreen
        tabbar.modalTransitionStyle = .crossDissolve
        present(tabbar, animated: true, completion: nil)
    }
```

#### โ ๋ค๋ฅธ ๊ณ์ ์ผ๋ก ๋ก๊ทธ์ธํ๋ ๊ธฐ๋ฅ ๊ตฌํํ๊ธฐ !

#### 1๏ธโฃ ์ฒ์์ ๋ด๊ฐ ์ง  ์ฝ๋

```swift
@IBAction func otherLoginButtonDidTap(_ sender: Any) {
        guard let naviVC = self.storyboard?.instantiateViewController(withIdentifier: "NavigationController")
                as? NavigationController else {return}

          naviVC.modalPresentationStyle = .fullScreen
          naviVC.modalTransitionStyle = .crossDissolve
          self.present(naviVC, animated: true, completion: nil)
    }
```

โ ๋ค๋ฅธ ๊ณ์ ์ผ๋ก ๋ก๊ทธ์ธ ํ๊ธฐ ๋ฒํผ์ ๋๋ฅผ ๊ฒฝ์ฐ, navigation controller๋ฅผ ๊ฐ์ ธ์ naviVC์ ์ ์ฅํ๋ค, ๋ชจ๋ฌ๋ก ๋ค์ ๋์์ฃผ๋ ๋ฐฉ์ ! ( fullscreen์ผ๋ก , ํจ๊ณผ๋ crossdissolve )

โ ๋จ์ํ ๋ก๊ทธ์ธ ํ๋ฉด ์ผ๋ก ๋์๊ฐ๋ฉด ๋ค์ ํ๋ฉด์ธ ํ์๊ฐ์ ์ฐฝ์ด ์ผ์ง์ง ์์ ! ์คํ์ด ์์ด์ง ์์ ..!! 

โ ๋ค๋น๊ฒ์ด์ ์ปจํธ๋กค๋ฌ๋ก ๋์๊ฐ์ผ ๋ก๊ทธ์ธ ์ฐฝ๋ถํฐ ํ์๊ฐ์ ์ฐฝ ๊น์ง ์คํ์ด ์์ !! 

---

#### 2๏ธโฃ ๋ค๋ฅธ ๋ฐฉ๋ฒ์ผ๋ก ์๋ !

๋ ์ฐพ์๋ณด๋ UINavigationController ํด๋์ค์ ๋ฉ์๋ ์ค์ popToRootViewController๋ฅผ ํตํด ๋ฃจํธ ๋ทฐ ์ปจํธ๋กค๋ฌ๊น์ง popํ  ์ ์์์ ! ํ์ง๋ง, ๋ฌธ์ ๋ present๋ก ๋์ด ๋ชจ๋ฌ์ฐฝ์ ์์ ์ผ pop์ด ์ ์์ ์ผ๋ก ์๋ ๋๋ค๋ ๊ฒ! 

- ์ฒซ ๋ฒ์งธ ์๋
    
    `self.navigationController?.popToRootViewController(animated: false)`
    
    ์ด๋ ๊ฒ๋ง ํด์ฃผ๋ฉด ์๋์ด ์๋จ.. 
    
- ๋ ๋ฒ์งธ ์๋
    
    ```swift
    self.dismiss(animated: true) {
    	self.navigationController?.popToRootViewController(animated: true)
    }
    ```
    
    ๋ ๋ฒ์งธ๋ก ์๋ํ๊ฑด dissmiss ํด์ฃผ๋ฉด์ ๋ฃจํธ ๋ทฐ ์ปจํธ๋กค๋ฌ๋ก ๋ฐ๋ก ๋์๊ฐ๊ฒ ํด์ฃผ๋ ๊ฒ ! 
    
    ๊ทผ๋ฐ ์ด๊ฒ๋ ์ ๋๋ก ์๋์ ํ์ง ์์์ ! ๊ทธ๋์ ์ฝ๋๋ฆฌ๋ทฐํ๋ฉด์ ์ค๋น ์ ๋ฐฐ๋ฆผ๋คํํ ์ฌ์ญค๋ด .! 
    

 ์ ํ ๊ณต์ ๋ฌธ์ ์ฐธ๊ณ  ! 

[Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uinavigationcontroller)

---

#### 3๏ธโฃ ํ๊ท์ ๋ฐฐ๋์ ์ฝ๋๋ฆฌ๋ทฐ ^^ ๋ฌดํํ ๊ฐ์ฌ๋ฅผ...

๐ย ๋ฃจํธ๋ทฐ๋ก ๋์๊ฐ๊ธฐ ์ํด์ย `popToRootViewController(animated:)`ย ๋ฉ์๋๋ฅผ ์๋ํ์๊ฑฐ๋ผ๊ณ  ์๊ฐํด์!dismiss ํ๊ฒ๋๋ฉด ํ์ฌ ๋ทฐ๊ฐ ๋ฉ๋ชจ๋ฆฌ ์์์ ์ฌ๋ผ์ง๋๋ค. ๊ทธ๋์ ์๋์ ์ฝ๋๋ฅผ ์ฌ์ฉํ๋ฉด ์ด๋ฏธ ์ฌ๋ผ์ง ํ์ฌ๋ทฐ์ navigationController ๋ฅผ ์ฐธ์กฐํ๊ฒ ๋๋ ๊ผด์ด๋์ฃ ! ์๋ง ์ฌ๊ธฐ๋ฅผ ๋์ณค์ ๊ฒ ๊ฐ์์

```swift
self.dismiss(animated: true) {
               self.navigationController?.popViewController(animated: true)
            }
```

๊ทธ๋์ย `guard let presentingVC = self.presentingViewController else { return }`ย ์ด๋ ๊ฒ ํ์ฌ ๋ทฐ์ปจํธ๋กค๋ฌ๋ฅผ ์ ๊ณตํ ๋ทฐ์ปจํธ๋กค๋ฌ ๊ฐ์ฒด๋ฅผ ๊ฐ์ ธ์์ presentingVC ๋ฅผ ๋์์ผ๋ก pop ์์ผ์ค์ผ ํ๋ต๋๋ค!

```swift
        guard let presentingVC = self.presentingViewController as? UINavigationController else { return }
        dismiss(animated: true) {
                presentingVC.popToRootViewController(animated: true)
            }
```

---

#### ๐ฎ ์ฝ๋๋ฆฌ๋ทฐ ๋ฐ์ํ๊ธฐ !

๊ฒฐ๋ก  ? ~~dissmiss ํ๋ ์๊ฐ ํ์ฌ ๋ทฐ๊ฐ ๋ฉ๋ชจ๋ฆฌ์์ ์ฌ๋ผ์ง๊ธฐ ๋๋ฌธ์ ! ํ์ฌ ๋ทฐ๋ฅผ ๋ค์ ๊ฐ์ ธ์์ ๊ทธ ๋ทฐ์์ ๋ฃจํธ ๋ทฐ ์ปจํธ๋กค๋ฌ๋ก popํด์ค์ผ๋๋ค~~

-> ์์  : ํ์ฌ ๋ทฐ๊ฐ ๋ฉ๋ชจ๋ฆฌ์์ ์ฌ๋ผ์ง๊ธฐ ๋๋ฌธ์ `self.navigationController?` ๊ฐ ๋น์ด์์ด์. ๊ทธ๋ฆฌ๊ณ  ์ ์ด์ present ๋ก ๋ทฐ๊ฐ ํ๋ฉด์ ํ๋์๊ธฐ ๋๋ฌธ์ viewDidLoad() ์์ ์ถ๋ ฅํด๋ณด์๋ ๋น์ด์์ต๋๋ค! push ๋ก ํ๋ฉด์ ํ์ ํ ๊ฒ์ด ์๋๊ธฐ ๋๋ฌธ์ด์ฃ ! ๊ทธ๋์ ์ด ๋ถ๋ถ์ dismiss ํ๋ฉด ๋ฉ๋ชจ๋ฆฌ์์ ๋ทฐ๊ฐ ํด์ ๋๋๋ฐ `self.` ๋ก ์ ๊ทผํ  ์ ์๋ ๊ฒ์ด ์๋ค! ๋ผ๊ณ  ์๊ฐํ์๋ฉด ๋ ๊ฑฐ๊ฐ์์๐

```swift
@IBAction func otherLoginButtonDidTap(_ sender: Any) {
        guard let presentingVC = self.presentingViewController as? UINavigationController else { return }
            self.dismiss(animated: true) {
                presentingVC.popToRootViewController(animated: true)
            }
    }
```
