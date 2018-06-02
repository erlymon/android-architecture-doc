# Определите общий destination для нескольких элементов пользовательского интерфейса

Вы можете использовать глобальный action для определения общего destination, к которому можно получить доступ несколькими элементами пользовательского интерфейса.
Например, вы можете нажать кнопку «Отмена» в нескольких разных destinations, чтобы перейти к тому же главному экрану приложения.

## Создание глобального action

Чтобы создать глобальный action:

1.  В Graph Editor нажмите на destination, для выделения destination.
2.  Кликнете правой кнопкой мыши по destination, для отображения контекстного меню.
3.  Выберите Add Action > Global. Слева от destination появится стрелка (![alt](https://developer.android.com/studio/images/buttons/navigation-globalaction.png)).
4.  Кликнете по вкладке _Text_, для перехода к текстовому виду XML. XML для глобального action выглядит следующим образом.

```xml
<action android:id="@+id/action_global_mainFragment"
    app:destination="@id/mainFragment"/>
```

## Использовать глобального action

Для использования глобального action в вашем коде, передайте идентификатор ресурса глобального action методу [navigate()](https://developer.android.com/reference/androidx/navigation/NavController.html#navigate(int)) для каждого элемента пользовательского интерфейса:

```kotlin
// kotlin
viewTransactionButton.setOnClickListener { view ->
    view.findNavController().navigate(R.id.action_global_mainFragment)
}
```

```java
// java
viewTransactionsButton.setOnClickListener(new View.OnClickListener() {
   @Override
   public void onClick(View view) {
       Navigation.findNavController(view).navigate(R.id.action_global_mainFragment);
   }
});
```
