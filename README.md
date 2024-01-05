<p>
  <h2>Material Theme Builder</h2>
  
  > [!NOTE]
  > 앱 색상 구성을 쉽고 빠르게 할 수 있도록 도와주는 도구: [사이트로 가기](https://m3.material.io/theme-builder#/custom)   
  >**Export 버튼**을 통해 Color.kt와 Theme.kt 파일들을 다운받을 수 있다. 

  ### 구성 별 기능
  - **primary**: UI에서 주요 구성요소에 사용된다.
  - **secondary**: UI에서 눈에 덜 띄는 구성요소에 사용된다.
  - **tertiary**: 기본 색상과 보조 색상의 균형을 맞추거나 입력란과 같은 특정 요소로 관심을 유도하는 데 사용할 수 있는 대비 강조를 위해 사용된다.
  - **on**: on이 붙은 요소들은 팔레트의 색상 위에 나타나며, 주로 텍스트, 아이콘, 획에 적용된다.
<br>
  <h2>Dimens 파일</h2>
  
  > [!NOTE]
  > 크기 값을 저장하기 위해 사용되는 파일  
  > 경로: **"app > res > values > dimens.xml"**

  - xml 파일에 저장하는 방법
    ```
    <resources>
     <dimen name="padding_small">8dp</dimen>
     <dimen name="padding_medium">16dp</dimen>
     <dimen name="image_size">64dp</dimen>
    </resources>
    ```
  - kt 파일에서 사용하는 방법
    ```
    modifier = Modifier.padding(dimensionResource(id = R.dimen.padding_small))
    ```
  
</p>
