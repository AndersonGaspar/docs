## Android Studio: ##

Ciclos de vida da Activity:

 ![ciclos.png](https://developer.android.com/guide/components/images/activity_lifecycle.png)
 
 Ao iniciar uma atividade, chama-se o método **onCreate()**(setContentView), ali é implementado o que for preciso para iniciar os componentes da atividade.
 
 Ao colocar o aplicativo em segundo plano ou rotacionar a tela, salva-se os estados da atividade no método **onPause()** que não é necessariamente uma destruição da atividade.
 
 Ao iniciar a atividade de segundo plano, chama-se o método **onStart()**, método de garantia que os conteúdos continuam disponíveis.
 
 Ao reiniciar uma Activity o método **onResume()** é acionado.
 
 Quando uma Activity não está sendo visualizada pelo usuário chama-se o método **onStop()** para liberar recursos
 
 O método **onDestroy** é chamado quando a Activity vai ser destruida.
 
 ### Links úteis:###
 
https://developer.android.com/guide/components/activities/?hl=pt-br

* caixa de dialogo:  

https://developer.android.com/guide/topics/ui/dialogs?hl=pt-br

* Menu lateral

https://developer.android.com/reference/android/support/design/widget/NavigationView
