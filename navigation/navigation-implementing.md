# Реализация навигации с помощью  Архитектурного Компонента Навигации

Архитектурный Компонент Навигации упрощает реализацию навигации между _destinations_ в вашем приложении.
Destination - это экран, который открывается в приложении.
По умолчанию Архитектурный Компонент Навигации использует фрагменты и активити, как destinations, но вы также можете
[добавить поддержку для новых типов destinations](https://developer.android.com/topic/libraries/architecture/navigation/navigation-add-new).
Набор адресатов представляет собой _навигационный граф_ приложения.

![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-graph.png "Изображение 1. Навигационный граф")

Архитектурный Компонент Навигации основан на [Принципах навигации](https://developer.android.com/topic/libraries/architecture/navigation/navigation-principles.html).

## Настройка навигации в проекте

Прежде чем создавать навигационный граф, вы должны настроить Архитектурный Компонент Навигации для своего проекта.
Для того чтобы настроить проект в Android Studio, необходимо выполнить следующие действия.

1.  Добавте следующий Архитектурный Компонент Навигации для вашего приложения или модуля в build.gradle файл.
    Дополнительные сведения о добавлении Архитектурного Компонента Навигации для build.gradle см. в разделе [Добавление компонентов в проект](https://developer.android.com/topic/libraries/architecture/adding-components#navigation).

2.  В окне «Проект», щелкните правой кнопкой мыши на каталоге res и выберите **New > Android resource file.** Появится диалог **New Resource**.

3.  Введите имя в поле **File name**, например **nav_graph**.

4.  Выберите **Navigation** в раскрывающемся списке **Resource type**.

5.  Нажмите **OK**. Произойдет следующие:

    -   В каталоге res появится каталог _navigation_.
    -   Файл nav_graph.xml создается в каталоге navigation.
    -   Файл nav_graph.xml открывается в редакторе navigation. Этот xml-файл содержит ваш навигационный граф.

6.  Перейдите на вкладку **Text**, чтобы переключиться на текстовое представление графа в XML. XML, для пустого навигационного графа, выглядит так:

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android">
</navigation>
```

7.  Щелкните на **Design**, чтобы вернуться к графическому редактору навигации.

## Обзор редактора навигации.

В Редакторе навигации вы можете быстро создавать граф навигации вместо создания графа руками в XML.
Как показано на рисунке 2, Редактор навигации имеет три раздела:

![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-editor.png "Изображение 2. Редактор навигации")

Секции Редактора навигации:

1.  **The Destinations list** - список всех destinations в Графическом Редакторе на текущий момент.
2.  **The Graph Editor** - содержит визуальное представление вашего навигационного графа.
3.  **The Attributes Editor** - cодержит атрибуты, связанные с destinations и actions в вашем графе навигации.

## Определить направление

Первым шагом в создании навигационного графа является определение destinations для вашего приложения.
Вы можете создавать пустые destinations или создавать destinations из фрагментов и активити в существующем проекте.

> Примечание: Архитектурный Компонент Навигации предназначен для приложений, которые имеют одно основное активити с несколькими destinations фрагментов.
> Основное активити «содержит» навигационный граф. В приложении с несколькими destinations активити, каждый дополнительный активити содержит свой собственный навигационный граф.
> Модификация активити для хост навигации обсуждается далее в этом документе.

Чтобы определить destinations для вашего приложения, выполните следующие действия.

1.  В редакторе графов нажмите **New Destination** ![alt text](https://developer.android.com/studio/images/buttons/navigation-add.png "New Destination"). Появится диалоговое окно **New Destination**.

2.  Нажмите **Create blank destination** или щелкните фрагмент или активити. Откроется диалоговое окно **New Android Component**.

3.  Введите имя в поле **Fragment Name**. Это имя является именем класса фрагмента.

4.  Введите имя в поле **Fragment Layout Name**. Это имя является именем файла макета для фрагмента.

5.  Нажмите **Finish**. В Graph Editor и в списке адресатов появится поле, представляющее адресат. Происходит следующее:
    -   Если вы создали пустой бланк destination, то Graph Editor покажет сообщение **Hello blank fragment** в destination.
        Если вы щелкнули по фрагменту или активити, Graph Editor покажет предварительный просмотр макета для этого активити или фрагмента.
    -   Для вашего проекта создан подкласс _Fragment_. Этот класс имеет имя, которое вы destination на шаге 3.
    -   Для вашего проекта создается файл resource. Этот файл имеет имя, указанное на шаге 4.

На рисунке 3 показан пустой и существующий пункт destination.
![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-newexisting.png "Изображение 3. Новые destinations в Graph Editor")

6.  Нажмите добавленный destination, чтобы выделить его. На панели «Attributes Editor» отображаются следующие атрибуты:

    -   Поле «Type» содержит «Fragment» или «Activity» - это показывает, в каком виде реализуется Destination в виде фрагмента или активити в исходном коде.
    -   Поле «Label» содержит имя destination.
    -   Поле ID содержит идентификатор destination, который будет использоваться для ссылки на destination в коде.
    -   Поле Class содержит имя класса для destination.

7.  Перейдите на вкладку «Text», чтобы перейти к представлению XML.
    Теперь XML содержит атрибуты идентификатор, имя (имя класса), метки и макета, основанные на именах существующих файлов классов и макетов:

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    app:startDestination="@id/blankFragment">
    <fragment
        android:id="@+id/blankFragment"
        android:name="com.example.cashdog.cashdog.BlankFragment"
        android:label="Blank"
        tools:layout="@layout/fragment_blank" />
</navigation>
```

> Примечание: XML имеет атрибут startDestination, указывающий на id нового пустого destination (app:startDestination="@+id/fragment").
> Для получения дополнительной информации о start destinations, см [Назначить экран в качестве start destination](https://developer.android.com/topic/libraries/architecture/navigation/Designate-start)

## Соединение destinations

У вас должно быть несколько destinations для соединения их между собой. Ниже приведен навигационный граф в XML с двумя пустыми destinations:

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    app:startDestination="@id/blankFragment">
    <fragment
        android:id="@+id/blankFragment"
        android:name="com.example.cashdog.cashdog.BlankFragment"
        android:label="fragment_blank"
        tools:layout="@layout/fragment_blank" />
    <fragment
        android:id="@+id/blankFragment2"
        android:name="com.example.cashdog.cashdog.BlankFragment2"
        android:label="Blank2"
        tools:layout="@layout/fragment_blank_fragment2" />
</navigation>
```

Destinations подключаются с помощью actions. Для подключения двух destinations:

1.  В Graph Editor наведите указатель мыши на правую сторону destination, из которого вы хотите перейти.
    В адресате появится круг.
    ![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-actioncircle.png "Изображение 4. Action connection circle")

2.  Нажмите и удерживайте левую кнопку, перетащите указатель мыши на destination, к которому вы хотите перейти, и отпустите.
    Отрисуется стрелка для указания навигации между двумя destinations.
    ![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-connected.png "Изображение 5. Connected destinations")


3.  Нажмите на стрелку, чтобы выделить action.
    В Attributes Editor отображаются следующие атрибуты:
        \- Поле «Type» содержит «Action».
        \- Поле ID содержит идентификатор, присвоенный системой для action.
        \- Поле Destination содержит идентификатор для destination фрагмента или активити.

4.  Перейдите на вкладку «Text», чтобы перейти к представлению XML.
    Action был добавлен в родительский адресат (destination).
    Action имеет назначенный системой идентификатор и атрибут destination, содержащий идентификатор следующего destination.
    Для примера:

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    app:startDestination="@id/blankFragment">
    <fragment
        android:id="@+id/blankFragment"
        android:name="com.example.cashdog.cashdog.BlankFragment"
        android:label="fragment_blank"
        tools:layout="@layout/fragment_blank" >
        <action
            android:id="@+id/action_blankFragment_to_blankFragment2"
            app:destination="@id/blankFragment2" />
    </fragment>
    <fragment
        android:id="@+id/blankFragment2"
        android:name="com.example.cashdog.cashdog.BlankFragment2"
        android:label="fragment_blank_fragment2"
        tools:layout="@layout/fragment_blank_fragment2" />
</navigation>
```

### Назначить destination в качестве start destination

Graph Editor помещает значок дома![alt text](https://developer.android.com/studio/images/buttons/navigation-house.png "Start Destination") рядом с именем первого destination в вашем приложении.
Этот значок указывает, что это стартовый destination в Навигационном Графе.
Вы можете назначить другой destination в качестве стартового destination, выполнив следующие шаги:

5.  В Graph Editor нажмите на destination. Destination выделен.

6.  Нажмите **Set Start Destination** на панели «Attributes Editor». Destination теперь является стартовым адресатом.

## Изменение activity к host navigation

Активити с host navigation реализует интерфейс [NavHost](https://developer.android.com/reference/androidx/navigation/NavHost.html), который добавляется в макет вашей активности.
[NavHost](https://developer.android.com/reference/androidx/navigation/NavHost.html) - это пустой вид, по которому destinations меняются местами и выходят, когда пользователь перемещается по вашему приложению.

Реализованной Архитектурный Компонент Навигации по умолчанию [NavHost](https://developer.android.com/reference/androidx/navigation/NavHost.html), является [NavHostFragment](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment.html).

После того, как вы включили [NavHost](https://developer.android.com/reference/androidx/navigation/NavHost.html), вы должны связать свой навигационный граф с [NavHostFragment](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment.html) с помощью атрибута _navGraph_.
Следующий фрагмент показывает, как включить [NavHostFragment](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment.html) и связать навигационный граф с этим NavHostFragment в файле макета активити:

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <fragment
        android:id="@+id/my_nav_host_fragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        app:navGraph="@navigation/nav_graph"
        app:defaultNavHost="true"
        />

</android.support.constraint.ConstraintLayout>
```

Предыдущий пример содержит _app:defaultNavHost="true"_ атрибут.
Этот атрибут гарантирует, что _NavHostFragment_ перехватит кнопку «Back button».
Вы также перопределите [AppCompatActivity.onSupportNavigateUp()](https://developer.android.com/reference/android/support/v7/app/AppCompatActivity) и вызовите [NavController.navigateUp()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigateUp()) следующим образом:

```kotlin
// Пример на kotlin:
override fun onSupportNavigateUp()
        = findNavController(R.id.nav_host_fragment).navigateUp()
```

```java
// Пример на java:
@Override
public boolean onSupportNavigateUp() {
    return Navigation.findNavController(this, R.id.nav_host_fragment).navigateUp();
}
```

## Привязка destinations к UI виджетам

Переход к destination осуществляется с использованием класса [NavController](https://developer.android.com/reference/androidx/navigation/NavController.html).
[NavController](https://developer.android.com/reference/androidx/navigation/NavController.html) может быть восстановлен с использованием одного из следующих статических методов:
[NavHostFragment.findNavController(Fragment)](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment.html#findNavController(android.support.v4.app.Fragment))
[Navigation.findNavController(Activity, @IdRes int viewId)](https://developer.android.com/reference/androidx/navigation/Navigation.html#findNavController(android.app.Activity,%20int))
[Navigation.findNavController(View)](https://developer.android.com/reference/androidx/navigation/Navigation.html#findNavController(android.view.View))

После того, как вы получите [NavController](https://developer.android.com/reference/androidx/navigation/NavController.html), используйте его метод [navigate()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigate(int)) для перехода к destination.
Метод [navigate()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigate(int)) принимает идентификатор ресурса. Идентификатор может быть идентификатором определенного destination в навигационном графе или action.
Использование идентификатора action вместо идентификатора ресурса destination имеет преимущества, такие как объединение переходов с вашей навигацией.
Подробнее о переходах см. в разделе [Create a transition between destinations](https://developer.android.com/topic/libraries/architecture/navigation/navigation-implementing#Create-transition).

В следующем фрагменте кода показано, как перейти к **ViewTransactionsFragment**:

```kotlin
// Пример на kotlin:
viewTransactionsButton.setOnClickListener { view ->
   view.findNavController().navigate(R.id.viewTransactionsAction)
}
```

```java
// Пример на java:
viewTransactionsButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Navigation.findNavController(view).navigate(R.id.viewTransactionsAction);
    }
});
```

Система Android поддерживает [back stack](https://developer.android.com/guide/components/activities/tasks-and-back-stack), содержащий последнее посещенное место destination.
Первый destination вашего приложения помещается в стек, когда пользователь открывает приложение.
Каждый вызов метода [navigate()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigate(int)) помещает следующий destination в верхнюю часть стека.
И наоборот, нажатие кнопки «Up» или «Back» вызывает методы [NavController.navigateUp()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigateUp()) и [NavController.popBackStack()](https://developer.android.com/reference/androidx/navigation/NavController.html#popBackStack()), соответственно, которые извлекают верхний destination из стека.

Для кнопок вы также можете использовать метод createNavigateOnClickListener() класса Navigation для перехода к destination:

```kotlin
// Пример на kotlin:
button.setOnClickListener(Navigation.createNavigateOnClickListener(R.id.next_fragment, null))
```

```java
// Пример на java:
button.setOnClickListener(Navigation.createNavigateOnClickListener(R.id.next_fragment, null));
```

### Привязки к компонентам меню пользовательского интерфейса

Вы можете привязать destinations к navigation drawer menu и overflow menu, используя идентификатор destination в качестве одного и того же идентификатора для элемента navigation drawer или overflow menu в XML.
В следующем фрагменте кода показан destination деталей с идентификатором - detail_page_fragment:

```xml
<fragment android:id="@+id/details_page_fragment"
     android:label="@string/details"
     android:name="com.example.android.myapp.DetailsFragment" />
```

Использование одного и того же идентификатора как для destination, так и для пункта меню автоматически связывает адресат с пунктом меню.
В следующем XML показано, как связать destination фрагмента с элементом меню в navigation drawer (например, menu_nav_drawer.xml):

```xml
<item
    android:id="@id/details_page_fragment"
    android:icon="@drawable/ic_details"
    android:title="@string/details" />
```

Следующий XML показывает, как связать destination деталей с overflow menu (например, menu_overflow.xml):

```xml
<item
    android:id="@id/details_page_fragment"
    android:icon="@drawable/ic_details"
    android:title="@string/details"
    android:menuCategory:"secondary" />
```

Архитектурный Компонент Навигации включает в себя класс [NavigationUI](https://developer.android.com/reference/androidx/navigation/ui/NavigationUI.html).
Этот класс имеет несколько статических методов, с помощью которых вы можете использовать пункты меню с destinations.
Например, следующий код показывает, как использовать метод [setupWithNavController()](https://developer.android.com/reference/androidx/navigation/ui/NavigationUI.html#setupWithNavController(android.support.design.widget.NavigationView,%20androidx.navigation.NavController)) для подключения элементов в menu drawer к [NavigationView](https://developer.android.com/reference/android/support/design/widget/NavigationView):

```kotlin
// Пример на kotlin:
val navigationView = findViewById(R.id.nav_view)
navigationView.setupWithNavController(navController)
```

```java
// Пример на java:
NavigationView navigationView = (NavigationView) findViewById(R.id.nav_view);
NavigationUI.setupWithNavController(navigationView, navController);
```

Необходимо настроить навигационные компоненты с помощью методов [NavigationUI](https://developer.android.com/reference/androidx/navigation/ui/NavigationUI.html), чтобы состояние элементов пользовательского интерфейса оставалось в синхронизации с изменениями [NavController](https://developer.android.com/reference/androidx/navigation/NavController.html).

## Передача данных между destinations

Вы можете передавать данные между destinations двумя способами: используя объекты Bundle или безопасным способом с использованием safeargs плагина для Gradle.
Используйте следующие шаги для передачи данных между destinations, используя объекты Bundle.
Если вы используете Gradle, рассмотрите следующие инструкции в [Передача данных между destinations безопасным способом]{#Arguments}.

1.  В Graph Editor нажмите на destination, в котором получен аргумент. Destination выделится.

2.  Нажмите **Add (+)** в  панели «Attributes Editor». Появятся пустые поля имени и значения по умолчанию.

3.  Дважды щелкните по имени и введите имя для аргумента.

4.  Нажмите Tab и введите значение по умолчанию для аргумента.

5.  Нажмите на action, предшествующее этому destination. Значения по умолчанию аргумента должны содержать ваш добавленный аргумент.

6.  Перейдите на вкладку «Text», чтобы перейти к представлению XML. Элемент аргумента с атрибутами name и defaultValue добавлен в destination:

```xml
<fragment
   android:id="@+id/confirmationFragment"
   android:name="com.example.cashdog.cashdog.ConfirmationFragment"
   android:label="fragment_confirmation"
   tools:layout="@layout/fragment_confirmation">
   <argument android:name="amount" android:defaultValue="0" />
```

7.  В своем коде создайте bundle и передайте его в destination с помощью метода [navigate()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigate(int)):

    ```kotlin
    // Пример на kotlin:
    var bundle = bundleOf("amount" to amount)
    view.findNavController().navigate(R.id.confirmationAction, bundle)
    ```

    ```java
    // Пример на java:
    Bundle bundle = new Bundle();
    bundle.putString("amount", amount);
    Navigation.findNavController(view).navigate(R.id.confirmationAction, bundle);
    ```

В коде destination получателя используйте метод [getArguments()](https://developer.android.com/reference/android/app/Fragment.html#getArguments()) для извлечения bundle и использования его содержимого:

```kotlin
// Пример на kotlin:
val tv = view.findViewById(R.id.textViewAmount)
tv.text = arguments.getString("amount")
```

```java
// Пример на java:
TextView tv = view.findViewById(R.id.textViewAmount);
tv.setText(getArguments().getString("amount"));
```

## Передача данных между destinations безопасным способом

 Архитектурный Компонент Навигации имеет плагин Gradle, называемый safeargs, который генерирует простые классы объектов и builder для безопасного доступа по типу к аргументам, указанным для destinations и actions.
 Safe args построены на основе подхода Bundle, но для получения большей безопасности типов требуется немного дополнительного кода.
 Если вы используете Gradle, вы можете использовать safe args плагин.
 Чтобы добавить этот плагин, добавьте плагин 'androidx.navigation.safeargs' в файл build.gradle.
 Для примера:

```gradle
apply plugin: 'com.android.application'
apply plugin: 'androidx.navigation.safeargs'

android {
   //...
}
```

 После настройки плагина Gradle выполните следующие действия, чтобы использовать type-safe args.

1.  В Graph Editor нажмите на адресат, в котором получен аргумент. Destination выделится.

2.  Нажмите **Add (+)** в  панели «Attributes Editor». Появятся пустые поля имени и значения по умолчанию.

3.  Дважды щелкните по имени и введите имя для аргумента.

4.  Нажмите «Tab» и выберите тип для аргумента в раскрывающемся списке.

5.  Нажмите Tab и введите значение по умолчанию для аргумента.

6.  Нажмите на action, предшествующее этому destination. Значения по умолчанию аргумента должны содержать ваш добавленный аргумент.

7.  Перейдите на вкладку «Text», чтобы перейти к представлению XML. Элемент аргумента с атрибутами name и defaultValue добавлен в destination:

```xml
<fragment
    android:id="@+id/confirmationFragment"
    android:name="com.example.buybuddy.buybuddy.ConfirmationFragment"
    android:label="fragment_confirmation"
    tools:layout="@layout/fragment_confirmation">
    <argument android:name="amount" android:defaultValue="1" app:type="integer"/>
</fragment>
```

Когда вы создаете код с помощью плагина safeargs, для action и sending и receiving destinations создаются простые классы объектов и builder классы.
Эти классы:

-   Класс для destination, в котором происходит action, прилагается к слову **«Directions»**.

    Итак, если исходный фрагмент называется SpecifyAmountFragment, сгенерированный класс называется **SpecifyAmountFragmentDirections**.
    Этот класс имеет метод, названный для action, используемого для передачи аргумента, для объединения аргумента, такого **confirmationAction()**.

-   Внутренний класс, имя которого основано на action, используемом для передачи аргумента.
    Если передающий action называется confirmAction, класс называется **ConfirmationAction**.

-   Класс для destionation, где передаются аргументы, добавляется со словом **Args**.

    Итак, если целевой фрагмент называется **ConfirmationFragment**, сгенерированный класс называется **ConfirmationFragmentArgs**.
    Используйте метод **fromBundle()** этого класса для извлечения аргументов.

Следующий код показывает вам, как использовать эти методы для установки аргумента и передать его методу [navigate()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigate(int)).

```kotlin
// Пример на kotlin:
override fun onClick(v: View?) {
  val amountTv: EditText = view!!.findViewById(R.id.editTextAmount)
  val amount = amountTv.text.toString().toInt()
  val action = SpecifyAmountFragmentDirections.confirmationAction(amount)
  action.amount = amount
  v.findNavController().navigate(action)
}
```

```java
// Пример на java:
@Override
public void onClick(View view) {
  EditText amountTv = (EditText) getView().findViewById(R.id.editTextAmount);
  int amount = Integer.parseInt(amountTv.getText().toString());
  ConfirmationAction action =
          SpecifyAmountFragmentDirections.confirmationAction()
  action.setAmount(amount)
  Navigation.findNavController(view).navigate(action);
}
```

В коде destination получателя используйте метод [getArguments()](https://developer.android.com/reference/android/app/Fragment.html#getArguments()) для извлечения bundle и использования его содержимого:

```kotlin
// Пример на kotlin:
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
   val tv: TextView = view.findViewById(R.id.textViewAmount)
   val amount = ConfirmationFragmentArgs.fromBundle(arguments).amount
   tv.text = amount.toString()
}
```

```java
// Пример на java:
@Override
public void onViewCreated(View view, @Nullable Bundle savedInstanceState) {
   TextView tv = view.findViewById(R.id.textViewAmount);
   int amount = ConfirmationFragmentArgs.fromBundle(getArguments()).getAmount();
   tv.setText(amount + "")
}
```

## Групповые destinations в вложенном навигационном графе

 Ряд destinations может быть сгруппирован в подграф в навигационном графе.
 Подграф называется **«nested graph»**, а содержащий граф называется **«root graph»**.
 Вложенные графы полезны для организации и повторного использования разделов пользовательского интерфейса вашего приложения, например, для separate login flow.

 Как и в случае с корневым графом, вложенный граф должен иметь destination, идентифицированный, как стартовый destination.
 Вложенный граф инкапсулирует его destinations; destinations за пределами вложенного графа, например, на корневом графе, только обращаются к вложенному графу через его начальное место назначения.
 На рисунке 6 показан граф навигации для простого приложения для перевода денег.
 Этот граф имеет два потока: поток, позволяющий пользователю отправлять деньги и поток, позволяющий пользователю просматривать их баланс

 ![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-pre-nestedgraph.png "Изображение 6. Money transfer navigation graph")

 Чтобы сгруппировать destinations во вложенный граф:

1.  В Graph Editor нажмите и удерживайте нажатой клавишу **shift** и выберите нужные destinations в вложенном графе. Каждый destination подсвечивается.

2.  Откройте контекстное меню и выберите **Move to Nested Graph > New Graph**.
    Destinations заключены в вложенный граф.
    На изображении 7 показан вложенный граф в Graph Editor.
    ![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-nestedgraph.png "Изображение 7. Вложенный граф в Graph Editor")

3.  Нажмите на вложенный граф, чтобы выделить его. На панели Attributes Editor отображаются следующие атрибуты:

-   Поле «Type» содержит «Nested Graph».
-   Поле ID содержит идентификатор, присвоенный системой для вложенного графа.
    Этот идентификатор используется для ссылки на вложенный граф внутри вашего кода.

4.  Дважды щелкните по вложенному графу. Появятся destinations в вложенном графе.

5.  В списке **Destinations** нажмите **Root**, чтобы вернуться к корневому графу навигации.

6.  Перейдите на вкладку **Text**, чтобы перейти к представлению XML.
    В корневой граф добавлен вложенный граф навигации.
    Этот навигационный граф имеет свои открытые и закрытые навигационные элементы.
    Этот вложенный граф имеет идентификатор sendMoneyGraph и атрибут startDestination, указывающий на стартовый destionation (chooseRecipient) во вложенном графе:

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   xmlns:android="http://schemas.android.com/apk/res/android"
   app:startDestination="@id/mainFragment">
   <fragment
       android:id="@+id/mainFragment"
       android:name="com.example.cashdog.cashdog.MainFragment"
       android:label="fragment_main"
       tools:layout="@layout/fragment_main" >
       <action
           android:id="@+id/action_mainFragment_to_chooseRecipient"
           app:destination="@id/sendMoneyGraph" />
       <action
           android:id="@+id/action_mainFragment_to_viewBalanceFragment"
           app:destination="@id/viewBalanceFragment" />
   </fragment>
   <fragment
       android:id="@+id/viewBalanceFragment"
       android:name="com.example.cashdog.cashdog.ViewBalanceFragment"
       android:label="fragment_view_balance"
       tools:layout="@layout/fragment_view_balance" />
   <navigation android:id="@+id/sendMoneyGraph" app:startDestination="@id/chooseRecipient">
       <fragment
           android:id="@+id/chooseRecipient"
           android:name="com.example.cashdog.cashdog.ChooseRecipient"
           android:label="fragment_choose_recipient"
           tools:layout="@layout/fragment_choose_recipient">
           <action
               android:id="@+id/action_chooseRecipient_to_chooseAmountFragment"
               app:destination="@id/chooseAmountFragment" />
       </fragment>
       <fragment
           android:id="@+id/chooseAmountFragment"
           android:name="com.example.cashdog.cashdog.ChooseAmountFragment"
           android:label="fragment_choose_amount"
           tools:layout="@layout/fragment_choose_amount" />
   </navigation>
</navigation>
```

7.  В своем коде передайте resource ID action, соединяющего корневой граф с вложенным графом:

    ```kotlin
    // Пример на kotlin:
    view.findNavController(view).navigate(R.id.action_mainFragment_to_sendMoneyGraph)
    ```

    ```java
    // Пример на java:
    Navigation.findNavController(view).navigate(R.id.action_mainFragment_to_sendMoneyGraph);
    ```

## Создание deep link для destination

В Android deep link - это URI, который указывает на конкретный destination в приложении.
Эти URI полезны, когда вы хотите отправить пользователей в определенный destination для выполнения какой-либо задачи в вашем приложении, например, денежный поток отправки, позволяющий пользователю быстро отправлять деньги кому-либо.

### Назначить deep link на destination

Чтобы назначить deep link на destination на вашем навигационном графе:

1.  В Graph Editor выберите destination для deep link.

2.  Нажмите **+** в разделе _Deep Links_ на панели «Атрибуты». Появится диалоговое окно **Add Deep Link**.

3.  Введите URI в поле URI, например «www.cashdog.com/sendmoney», который представляет собой стартовый destination вложенного графа в приложении.
    Обратите внимание на следующее:

    -   URI без схемы предполагаются как http и https. Например, www.cashdog.com соответствует <http://www.cashdog.com> и <https://www.cashdog.com>.
    -   Заполнитель в форме {placeholder_name} соответствует 1 или более символам.
        Значение String placeholder доступно в аргументах Bundle с ключом с тем же именем.
        Например, <http://www.example.com/users/{id}> соответствует <http://www.example.com/users/4>.
    -   .\* wildcard можно использовать для соответствия 0 или более символов.

4.  (необязательно). Проверьте **Auto Verify**, чтобы потребовать от Google подтверждения того, что вы являетесь владельцем URI. Для получения дополнительной информации см. [Подтвердить ссылки на приложения для Android](https://developer.android.com/training/app-links/verify-site-associations.html).

5.  Нажмите **Add**. Над выбранным destination появляется значок ссылки![alt text](https://developer.android.com/studio/images/buttons/navigation-deeplink.png "Link"), указывающий, что у destination есть deep link.

6.  Перейдите на вкладку «Text», чтобы перейти к представлению XML. Deep link добавлен в destination:

```xml
<deepLink app:uri="https://cashdog.com/sendmoney"/>
```

Когда пользователь использует Back button из destination deep link, они перемещаются обратно в стек навигации так же, как если бы они ввели ваше приложение из точки входа приложения.

### Добавьте intent filter для глубокой ссылки

Вы должны внести дополнения в свой файл manifest.xml, чтобы включить deep link в вашем приложении:

-   Для Android Studio 3.0 и 3.1 вы должны вручную добавить элемент intent-filter. Для получения дополнительной информации см. Раздел [Создание глубоких ссылок на контент приложения](https://developer.android.com/training/app-links/deep-linking.html).

-   Для Android Studio 3.2+ вы можете добавить элемент nav-graph элемента в свои активити:

```xml
<activity name=".MainActivity">
    <nav-graph android:value="@navigation/main_nav" />
</activity>
```

На этапе слияния манифеста, при сборке, этот элемент заменяется сгенерированными элементами, необходимыми для соответствия всем глубоким ссылкам на графе навигации.

## Создание перехода между destinations

Архитектурный Компонент Навигации обеспечивает функциональность, позволяющую легко добавлять переходы, такие как fade-in и fade-out, между destinations. Чтобы добавить переход:

1.  Создайте свои файлы ресурсов анимации. Для получения дополнительной информации см. [Declare анимации в XML](https://developer.android.com/guide/topics/graphics/prop-animation.html#declaring-xml).

2.  В Graph Editor нажмите на action, в котором должен произойти переход.

3.  В разделе «Transitions» панели «Attributes Editor» нажмите стрелку «down» рядом с «Enter». Появится список переходов в вашем проекте.

4.  Выберите переход, который должен произойти, когда пользователь входит в destination.

5.  В разделе «Transitions» панели «Attributes Editor» нажмите стрелку «вниз» рядом с «Exit». , Появится список переходов в вашем проекте.

6.  Выберите переход, который должен произойти, когда пользователь выйдет из destination.

7.  Перейдите на вкладку «Text», чтобы переключиться на текстовое представление XML.
    XML для перехода появляется в элементе action, указанного на шаге 2.
    Action внедрено в XML для destination, который активен до перехода.
    В следующем примере _specifyAmountFragment_ является активным местом destination и содержит action с анимацией перехода:

```xml
<fragment
    android:id="@+id/specifyAmountFragment"
    android:name="com.example.buybuddy.buybuddy.SpecifyAmountFragment"
    android:label="fragment_specify_amount"
    tools:layout="@layout/fragment_specify_amount">
    <action
        android:id="@+id/confirmationAction"
        app:destination="@id/confirmationFragment"
        app:enterAnim="@anim/slide_in_right"
        app:exitAnim="@anim/slide_out_left"
        app:popEnterAnim="@anim/slide_in_left"
        app:popExitAnim="@anim/slide_out_right" />
 </fragment>
```

В этом примере у нас есть переходы, которые срабатывают при переходе в пункт назначения (_enterAnim_ и _exitAnim_ и при выходе из этого пункта назначения (_popEnterAnim_ и _popExitAnim_).

## Что дальше

В этом документе объяснены основы для внедрения навигации. Доступны следующие дополнительные темы по навигации:

-   [Миграция к Архитектурному Компоненту Навигации](https://developer.android.com/topic/libraries/architecture/navigation/navigation-migrate.html)
-   [Добавить поддержку для новых типов адресатов](https://developer.android.com/topic/libraries/architecture/navigation/navigation-add-new.html)
-   [Внедрение условной навигации](https://developer.android.com/topic/libraries/architecture/navigation/navigation-conditional.html)
-   [Identify a common destination for several UI elements](https://developer.android.com/topic/libraries/architecture/navigation/navigation-global-action.html)
