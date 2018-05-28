# Добавить поддержку для новых типов destinations

[NavControllers](https://developer.android.com/reference/androidx/navigation/NavController.html) полагаются на один или несколько объектов [Navigator](https://developer.android.com/reference/androidx/navigation/Navigator.html) для выполнения операции навигации.
По умолчанию все [NavControllers](https://developer.android.com/reference/androidx/navigation/NavController.html) поддерживают выход из навигационного графа, переходя к другому activity с использованием класса [ActivityNavigator](https://developer.android.com/reference/androidx/navigation/ActivityNavigator.html) и его вложенного класса [ActivityNavigator.Destination](https://developer.android.com/reference/androidx/navigation/ActivityNavigator.Destination.html).
Чтобы иметь возможность перемещаться по любому другому destination, необходимо добавить один или несколько дополнительных объектов [Navigator](https://developer.android.com/reference/androidx/navigation/Navigator.html) в [NavController](https://developer.android.com/reference/androidx/navigation/NavController.html).
Например, при использовании фрагментов в качестве адресатов [NavHostFragment](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment.html) автоматически добавляет класс [FragmentNavigator](https://developer.android.com/reference/androidx/navigation/fragment/FragmentNavigator.html) в свой [NavControllers](https://developer.android.com/reference/androidx/navigation/NavController.html).

Для того чтобы добавить новый объект Navigator к [NavControllers](https://developer.android.com/reference/androidx/navigation/NavController.html), вы должны использовать соответствующий метод [getNavigatorProvider()](https://developer.android.com/reference/androidx/navigation/NavController.html#getNavigatorProvider()) класса Navigator, а затем метод [addNavigator()](https://developer.android.com/reference/androidx/navigation/NavigatorProvider.html) класса.
Следующий код показывает пример добавления вымышленного объекта CustomNavigator в [NavControllers](https://developer.android.com/reference/androidx/navigation/NavController.html):

```kotlin
// kotlin
val customNavigator = CustomNavigator()
navController.navigatorProvider += customNavigator
```

```java
// java
CustomNavigator customNavigator = new CustomNavigator();
navController.getNavigatorProvider().addNavigator(customNavigator);
```

Большинство классов [Navigator](https://developer.android.com/reference/androidx/navigation/Navigator.html) имеют вложенный подкласс destination.
Этот подкласс может использоваться для указания дополнительных атрибутов, уникальных для вашего destination.
Для получения дополнительной информации о подклассах Destination, см. справочную документацию для соответствующего класса [Navigator](https://developer.android.com/reference/androidx/navigation/Navigator.html).
