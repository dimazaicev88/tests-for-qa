# Тестовые задание для Java junior


**Задание 1**:
Используя Java Dynamic Proxy (https://docs.oracle.com/javase/8/docs/technotes/guides/reflection/proxy.html)
реализуйте метод
 ``` java
 MainPage createPage(Class clazz)
 ```
таким образом что бы проходил тест:
``` java

@Retention(java.lang.annotation.RetentionPolicy.RUNTIME)
@Target({METHOD, TYPE})
public @interface Selector {

    String xpath();
}

public interface MainPage {

    @Selector(xpath = ".//*[@test-attr='input_search']")
    String textInputSearch();

    @Selector(xpath = ".//*[@test-attr='button_search']")
    String buttonSearch();
}

public class MethodInterception {

    @Test
    public void annotationValue() {
        MainPage mainPage = createPage(MainPage.class);
        assertNotNull(mainPage);
        assertEquals(mainPage.buttonSearch(), ".//*[@test-attr='button_search']");
        assertEquals(mainPage.textInputSearch(), ".//*[@test-attr='input_search']");
    }

    private MainPage createPage(Class clazz) {
        return null;
    }
}
```

**Задание №2 - TestNG,ServiceLoader**:
Реализуйте перехват параметров анотации TestMethodInfo  в тестовом методе и вывод их в консоль. Подключение TestNg Listener нужно сделать через ServiceLoader. 
 ``` java

public enum Priority {
    Blocker, Critical, Major, Minor
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE) //on class level
public @interface TestMethodInfo {

//Приоритет теста
Priority priority() default Priority.Major;

//Автор теста	
String author() default "Bill Gates";

//Дата последних изменений в тесте
String lastModified() default "01.01.2019";
}

@Test
@TestMethodInfo(priority = Priority.Critical, author = "Test user", lastModified = "20.08.2019")
public void annotation() {
    assertEquals(1, 1);
}
```



**Результат выполнения задания нужно будет оформить на https://github.com/. В качестве ответа не нужно присылать ZIP архивов и наборов файлов, вы присылаете только ссылку на ваш репозиторий.**
