


### ๐ 1์ฃผ์ฐจ ๊ณผ์  ๋ฆฌ๋๋ฏธ
<br/>

- [X] UI ๊ตฌ์ฑํ๊ธฐ    
- [X] ํ๋ฉด์ ํํ๊ธฐ    
- [X] ๊ธฐ๋ฅ๊ตฌํํ๊ธฐ   
- [X] ๋์ ๊ณผ์  1   
- [X] ๋์ ๊ณผ์  2 
<br/>  

![Simulator Screen Recording - iPhone 13 - 2021-10-08 at 13 37 26](https://user-images.githubusercontent.com/81313960/136499805-965e0a1c-1f46-40df-8100-d1cdbd8b2def.gif)   


๊ตฌํ.. ํ๋ฉด .. ( ์๋ง์ง์ฐฝ ui๋ ๋ค์์ฃผ ์คํ ๋ ์ด์์ ๋ฐฐ์ฐ๋ฉด์ ์์ ํด๋ณด๊ฒ ์๋๋ค ํ์ดํ ! ) 


<br/>

#### ๐ฆ ํ๋ฉด์ ํํ๊ธฐ
- ๋ก๊ทธ์ธ, ํ์๊ฐ์ ํ๋ฉด -> ํ์ํฉ๋๋ค ํ๋ฉด : ๋ชจ๋ฌ ๋ฐฉ์์ผ๋ก ๊ตฌํ ( present )


```swift
@IBAction func nextButton(_ sender: Any) {
        guard let welcomeVC = self.storyboard?.instantiateViewController(withIdentifier:
        "WelcomeViewController") as? WelcomeViewController else {return}
        
        welcomeVC.userName = nameTextField.text
        welcomeVC.modalPresentationStyle = .fullScreen
        self.present(welcomeVC, animated: true, completion: nil)
        
    }
```    
<br/>

- ๋ก๊ทธ์ธ ํ๋ฉด์ ๊ณ์ ๋ง๋ค๊ธฐ ๋ฒํผ -> ํ์๊ฐ์ ํ๋ฉด : ๋ค๋น๊ฒ์ด์ ๋ฐฉ์์ผ๋ก ๊ตฌํ ( push )


```swift
@IBAction func nextButton(_ sender: UIButton) {
        guard let welcomeVC = self.storyboard?.instantiateViewController(withIdentifier: 
        "WelcomeViewController") as? WelcomeViewController else {return}
        
        welcomeVC.userName = nameTextField.text
        welcomeVC.modalPresentationStyle = .fullScreen
        self.present(welcomeVC, animated: true, completion: nil)
    }
```
<br/>



#### ๐ฆ ๊ธฐ๋ฅ๊ตฌํํ๊ธฐ
- ๋ก๊ทธ์ธ, ํ์๊ฐ์ ํ๋ฉด์์ ์ ๋ฌ๋ฐ์ userName ํ๋กํผํฐ๋ฅผ ํ์ํฉ๋๋ค ํ๋ฉด์ ํ์๋ฉ์์ง์ ํจ๊ป ๋์์ฃผ๊ธฐ 
- ๋ฌธ์์ด ๋ณด๊ฐ๋ฒ์ ์ฌ์ฉํ์ฌ ํ์๋ฉ์ธ์ง ํ์ 


```swift 
    var userName: String?
    
    // MARK: Life Cycle
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setUserNameInLabel()
    }
    
    // MARK: - Methods
    // MARK: Custom Method
    
    func setUserNameInLabel() {
        if let user = userName {
            welcomeLabel.text = "\(user)๋ ํ์ํฉ๋๋ค!"
            welcomeLabel.sizeToFit()
        }
    }
 ```
 
<br/>


#### ๐ย ๋์ ๊ณผ์  2 

- ํ์๊ฐ์ ํ๋ฉด์์ ๋น๋ฐ๋ฒํธ ํ์๋ฅผ ๋๋ฅผ ๊ฒฝ์ฐ ๋น๋ฐ๋ฒํธ๊ฐ ํ์๋๋๋ก ๊ตฌํํ๊ธฐ

```swift
@IBAction func showPasswordButton(_ sender: UIButton) {
        sender.isSelected = !sender.isSelected
        
        if sender.isSelected {
            passwordTextField.isSecureTextEntry = false
            showPasswordButton.setImage(UIImage(systemName: "checkmark.square" ), for: .selected)
        } else {
            passwordTextField.isSecureTextEntry = true
            showPasswordButton.setImage(UIImage(systemName: "square"), for: .normal)
        }
    }
```
1. ๋น๋ฐ๋ฒํธ ํ์ ๋ฒํผ์ ๋๋ฅผ ๊ฒฝ์ฐ ์ํธํ(?)๋ ๋ถ๋ถ์ด ํด์ (false)๋๊ณ , ๋ฒํผ ์ด๋ฏธ์ง๋ฅผ ๊ธฐ๋ณธ ๋ด์ฅ ์์ด์ฝ์ธ `checkmark.squre` ๋ก ๋ณ๊ฒฝ
2. ์ ํ๋ ์ํ์์ ๋ค์ ๋๋ฅผ ๊ฒฝ์ฐ ์๋ ์ํ๋ก ๋์์ค๋๋ก ๊ตฌํ 
3. ์๋ก ์๊ฒ๋ ๋ถ๋ถ : ๊ธฐ๋ณธ ๋ด์ฅ ์์ด์ฝ ์ฌ์ฉ์ `systemName:` ์ต์์ ์ฌ์ฉ ! 


<br/>

#### ๐ฑ ๊ธ์๋ํ - ๋์ ๊ณผ์  1 ์์  

- OB๋ถ๋ค์ ์ฝ๋๋ฆฌ๋ทฐ๋ฅผ ์ ๊ทน ๋ฐ์ํ์ฌ ์์ ํ ์ฌํญ์๋๋ค ( ๋ฉ์๊ณ  ๋ ๋ ํ ์ค๋น๋ถ๋..๐ )     
- ๋ค์์ฃผ ์ฝ๋๋ฆฌ๋ทฐ์ ๋ฐ์ : ์ฝ๋ฉ์ปจ๋ฒค์ ์ฝ์ด๋ณด๊ณ  ์ฐธ๊ณ ํด์ ์ฝ๋์ง๊ธฐ 

<br/>
   
๐ ๊ธ์๋ F4 ์ด์ ํ๊ท ์ ๋ฐฐ์ ์ฝ๋๋ฆฌ๋ทฐ : **๋์ ๊ณผ์ 1** ์์ ํ์คํธ ํ๋๊ฐ ๊ฐ์ด ์๋์ง ์๋์ง ํ์ธํ๋ ๋ถ๋ถ 

1. `nameTextField.hasText` : ํ์คํธ๋ฅผ ๊ฐ์ก๋ค๋ฉด true ๊ฐ์ ๊ฐ์ง๋ ํ๋กํผํฐ
2. `nameTextField.text!.isEmpty` : String ์ด Character ๋ฅผ ๊ฐ์ง์ง ์์๋ค๋ฉด true ๊ฐ์ ๊ฐ์ง๋ ํ๋กํผํฐ์๋๋ค. ์ฆ, ๋น์๋ค๋ฉด true! 



```swift
@objc func textFieldDidEndEditing(_ textField: UITextField) {
        if nameTextField.hasText && emailTextField.hasText && passwordTextField.hasText {
            nextButton.isEnabled = true
        } else {
            nextButton.isEnabled = false
        }
    }
```
- ์ ๋ถ ํ์คํธ ๊ฐ์ด ์์ ๋ ๋ฒํผ์ ํ์ฑํ์ํค๋๋ก `hasText` ์ฌ์ฉํด์ ๋ค์ ์์ ํด๋ดค์ต๋๋ค ! 


