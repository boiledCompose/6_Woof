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
  <h2>dimens.xml</h2>
  
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

  <br>
  <h2>Shape.kt</h2>

  > [!NOTE]
  > 구성요소의 테두리 모양/도형을 정의하는데 사용되는 파일 [상세보기](https://m3.material.io/styles/shape/shape-scale-tokens#b09934f1-1b0f-4ce4-ade6-4a1f138add6c)   
  > 경로: **"app > src > project ... package > ui.theme > Shape.kt"**
   

  - 구성요소는 소형, 중형, 대형의 세 가지 유형이 있다. 각각에 대해 도형 모양을 지정할 수 있다. 유형에 맞는 구성 요소들은 자동으로 모양이 바뀐다.
    ```
    val Shapes = Shapes(
      small = RoundedCornerShape(50.dp),
      medium = RoundedCornerShape(40.dp, 30.dp, 20.dp, 0.dp),
      large = RoundedCornerShape(10.dp)
    )
    ```
  - 사용자가 직접 `modifier`를 통해 모양을 지정할 수 있다.
    ```
    //여기서 MaterialTheme은 테마 이름으로, Theme.kt에 작성된 테마 객체다.
    
    modifier.clip(MaterialTheme.shapes.small)
    ```
  - 이미지의 경우, 바뀐 모양에 이미지를 맞추려면 contentScale 요소를 사용하면 된다.
    ```
    Image(
      ...,
      contentScale = ContentScale.Crop
    )
    ```

  <br>
  <h2>서체와 Typography</h2>
  
  > [!NOTE]
  > 서체 파일인 ttf 파일을 font 디렉토리에 저장하고, ttf 파일을 Type.kt에 객체화하여 사용할 수 있다.
  > 경로: **"app > src > project ... package > ui.theme > Type.kt"**
  > [서체 다운로드 사이트](https://fonts.google.com/?hl=ko)  

  - 저장된 폰트를 FontFamily 객체로 선언한다.
    ```
    //Type.kt
    val AbrilFatface = FontFamily(
      Font(R.font.abril_fatface_regular)
    )
    ```
  - 스타일에 따라 다른 폰트를 불러올 수 있도록 조정할 수 있다.
    ```
    val Montserrat = FontFamily(
      Font(R.font.montserrat_regular),
      Font(R.font.montserrat_bold, FontWeight.Bold)
    )
    ```
  - **Typography** 객체에는 13가지 서체를 위한 매개변수가 있다.
    ![image](https://github.com/boiledCompose/Woof/assets/101652649/1b69b8ab-6867-4c8b-a797-b60478612a80)
    
  - 객체 선언 시 매개변수 별로 TextStyle을 지정할 수 있다.
    ```
    val Typography = Typography(
      displayLarge = TextStyle(
        fontFamily = AbrilFatface,
        fontWeight = FontWeight.Normal,
        fontSize = 36.sp
      ),
      displayMedium = TextStyle(
        fontFamily = Montserrat,
        fontWeight = FontWeight.Bold,
        fontSize = 20.sp
      ),
      labelSmall = TextStyle(
        fontFamily = Montserrat,
        fontWeight = FontWeight.Bold,
        fontSize = 14.sp
      ),
      bodyLarge = TextStyle(
        fontFamily = Montserrat,
        fontWeight = FontWeight.Normal,
        fontSize = 14.sp
      )
    )
    ```
  - 텍스트의 **style 요소**을 통해 TextStyle을 지정할 수 있다.
    ```
    Text(
           text = "Hello World",
           style = MaterialTheme.typography.displayMedium,
    )
    ```
    
  <br>
  <h2>상단 바</h2>

  <h3>Scaffold</h3>

  > [!NOTE]
  > 다양한 구성요소와 화면 요소의 슬롯을 제공하는 레이아웃이다.   
  > Scaffold는 contentWindowInsets 매개변수를 지원한다. 이는 화면에서 앱이 시스템 UI와 교차할 수 있는 부분이다. [상세보기](https://developer.android.com/develop/ui/views/layout/insets?hl=ko)

  - 예제 코드
    ```
    @Composable
    fun WoofApp() {
       Scaffold(
           topBar = {
               WoofTopAppBar()
           }
       ) { it ->
           LazyColumn(contentPadding = it) {
               items(dogs) {
                   DogItem(
                       dog = it,
                       modifier = Modifier.padding(dimensionResource(id = R.dimen.padding_small))
                   )
               }
           }
       }
    }

    @Composable
    fun WoofTopAppBar(modifier: Modifier = Modifier) {
       CenterAlignedTopAppBar(
           title = {
               Row(
                   verticalAlignment = Alignment.CenterVertically
               )  {
                   Image(
                       modifier = Modifier
                           .size(dimensionResource(id = R.dimen.image_size))
                           .padding(dimensionResource(id = R.dimen.padding_small)),
                       painter = painterResource(R.drawable.ic_woof_logo),
      
                       contentDescription = null
                   )
                   Text(
                       text = stringResource(R.string.app_name),
                       style = MaterialTheme.typography.displayLarge
                   )
               }
           },
           modifier = modifier
       )
    }
    ```
</p>
