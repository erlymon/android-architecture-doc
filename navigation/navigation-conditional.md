# Внедрение условной навигации

У вашего приложения может быть ряд условных destinations, которые используются только в определенных условиях, например, когда пользователь должен войти в систему.
Эти destinations должны быть созданы как отдельные destinations или вложенные навигационные графы, которые при необходимости запускает другой destination.
На рисунке 1 показано, как пользователь переходит к destination профиля, который, определив, что пользователь не вошел в систему, требует, чтобы пользователь перешел к destination входа.
После того, как  пользователь авторизуется, destination «Вход» возвращает пользователя обратно в destination «Профиль».

![alt](https://developer.android.com/images/topic/libraries/architecture/navigation-conditional-graph.png "Figure 1. Conditional navigation.")

Destination входа должен удалиться из навигационного стека после того, как он вернется в destination «Профиль».
Вызовите метод [popBackStack()](https://developer.android.com/reference/androidx/navigation/NavController.html#popBackStack()) при переходе к исходному destination.
Исходный destination будет «удаляться» из навигационного стека и станет активным.
