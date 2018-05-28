# Миграция к Архитектурному Компоненту Навигации

NavController и его навигационный граф находится в пределах одного activity.
Следовательно, при миграции существующего проекта к использованию Архитектурного Компонента Навигации, сосредоточьтесь на переносе одного Activity за раз, создав навигационный граф для destinations в рамках каждого Activity.

![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-migrate1.png "Figure 1. Activities and their individual navigation graphs.")

Затем отдельные Activities можно связать, добавив activity destinations в навигационный граф, заменяя существующие методы startActivity() по всей базе кода.

![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-migrate2.png "Figure 2. Navigation graph in one Activity pointing to second Activity.")

В случаях, когда несколько Activities имеют один и тот же макет, графы навигации могут быть объединены, заменяя навигационные вызовы на activity destination, чтобы осуществлять переадресацию вызовов непосредственно между двумя навигационными графами.

![alt text](https://developer.android.com/images/topic/libraries/architecture/navigation-migrate3.png "Figure 3. Activity with combined navigation graph.")
